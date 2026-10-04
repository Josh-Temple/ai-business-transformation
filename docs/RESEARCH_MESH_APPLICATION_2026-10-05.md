# Research Mesh transferable findings — 2026-10-05

確認日：2026-10-05 JST  
適用先：AI Business Transformation  
性格：research support record / snapshot。Research Meshの現在状態そのものの正本ではない。

## 1. この記録の目的

2026-10-04〜05にResearch Meshで発生したquestion identity / lineage conflictから、複数AI・予定実行・versioned historyを使う業務システムへ再利用できる設計知見を抽出する。

ここには、scheduled taskの現在prompt、task ID、最新owner、Research Boardの現在行、Library receipt全文など、高頻度に変わるoperational stateは複製しない。

記録するのは次のような、時間が経っても再利用価値がある知見だけである。

- identityとexecution instanceを分ける設計
- versioned durable historyでの訂正方法
- lineage conflict時のfail-closed
- projectionとdurable historyの役割分離
- reader側まで含めたmigration / correctionの完了条件

---

## 2. 観測した失敗パターン

Research Meshでは、一度使われた研究Question IDが後から別テーマへ再利用され、同一stable identityの下に意味の異なる研究系列が存在する状態が発生した。

最初の修復では、Board上の表示を戻し、後発系列を別IDへ振り替え、誤ったreceiptの現在版をSUPERSEDED相当に扱った。

しかし、versioned durable historyでは過去version自体が検索対象として残るため、後続agentがfresh readすると、同じstable identityに異なる内容が存在することを再び検出した。agentがfail-closedしたこと自体は正しかった。

この事例から、**current objectの上書き・削除と、durable history上のidentity訂正は別問題**だと分かった。

---

## 3. 再利用可能な設計原則

### 3.1 stable identityとexecution identityを分離する

少なくとも次を別概念として扱う。

- **stable_id**: 問い・作業・研究系列そのものの恒久的identity
- **run_id**: 一回の実行・receipt・attemptのidentity
- **parent_run_id**: 実行系列の親子関係
- **provenance**: 過去の関連Evidenceや移行前系列への参照
- **projection**: Boardやdashboard上の現在表示

run filename、timestamp、Board row、latest updateだけからstable identityを逆算しない。

### 3.2 versioned historyでは「削除」ではなく明示的な訂正記録が必要

immutable / versioned storageでは、現在版を削除・上書きしても過去versionが監査履歴として残り得る。

そのため、identity事故を修復するには、少なくとも次のようなfirst-class correction recordが必要になる。

- 誤ったexact run identity
- 誤って使われたstable identity
- そのrunをactive lineageから除外する明示的disposition
- 正しいcanonical replacement
- 訂正のauthority
- 訂正が適用されるscope
- 未登録の競合は引き続きfail-closedとする境界

重要なのは「古い記録を見なかったことにする」のではなく、**監査履歴として保持しつつ、active lineage interpretationからだけ除外する**ことである。

### 3.3 correctionはexact-matchで限定し、一般化しすぎない

一つのknown bad runを訂正したからといって、似た名前・近い時刻・同じテーマの別runまで自動無効化しない。

安全な補正は、

> このexact run / exact identity combinationだけをaudit-onlyとする

という限定的な形にする。

それ以外の未知のidentity conflictは従来どおりfail-closedにする。

### 3.4 汚染されたlineageをclean rekeyする場合、provenanceとparent lineageを分ける

過去の系列そのものにidentity contaminationが残り、履歴を書き換えずに完全修復できない場合、新しい未使用stable identityへrekeyする方法がある。

このとき、新系列を過去の誤系列の子としてつなぐと、同じ汚染を引き継ぐ可能性がある。

そのため、

- 新stable identityはclean top-levelとして開始する
- 過去系列の科学的・業務的Evidenceはprovenanceとして参照する
- 過去runを新系列のlineage parentにしない
- 移行元はterminal / provenance-onlyとして閉じる

という分離が有効だった。

これは「過去Evidenceを捨てる」こととは異なる。

### 3.5 projectionだけ直しても修復は完了しない

Board / dashboardは現在状態のprojectionとして有用だが、durable historyの意味を上書きする正本にはしない。

Board上で一意に見えていても、durable history上で複数identity候補が残っていれば、fresh readerは競合を再発見する。

したがって、

- durable history
- identity correction
- current projection

を別層として扱う。

### 3.6 writer側の修復だけでは不十分で、reader側もcorrectionを解釈する必要がある

今回の重要な失敗は、Library / Boardを修復しても、scheduled agentのlineage reconstruction ruleが訂正記録を先に読まなければ、過去versionを再度active候補として扱う点だった。

つまりmigration / correctionの完了条件は、

1. correction recordを作る
2. canonical identityをrekey / reconcileする
3. projectionを更新する
4. **全readerがcorrection semanticsを理解する**
5. readbackで再構成結果を確認する

まで含む。

データ移行だけ済ませてconsumerを更新しない状態は、修復途中である。

---

## 4. fail-closedで維持すべき条件

以下はidentity解決ルールとして採用しない。

- timestampが新しい方を自動的にcanonicalとする
- Boardに一行しかないことを一意性の証明にする
- filename内のIDをstable_idとみなす
- 内容が似ていることを理由に系列をmergeする
- chat memoryや過去summaryをfresh canonical stateより優先する
- known correctionを別のunknown conflictへ類推適用する
- conflicting branchesを自動で一つへ畳み込む

明示的なcorrectionで解決できないmaterial identity conflictは、人間判断または別のauthoritative correctionまでfail-closedとする。

---

## 5. 複数agent / scheduled workflowへの実装含意

この知見はResearch Mesh固有に限らず、複数agentが共有状態を読むシステムへ一般化できる。

候補となる構造は次のとおり。

- task / questionにstable identityを持たせる
- executionごとに別run identityを持たせる
- immutable attempt logとcurrent projectionを分ける
- correction / tombstoneをfirst-class recordにする
- correctionはexact targetとscopeを持つ
- agentはcurrent projectionだけでなくcorrection registryをidentity reconstruction前に読む
- unmatched ambiguityではside effectを止める
- migration後はwriterだけでなくreader全体をreadbackする

特に、event-sourced / append-only / versioned storageでは、**「消したから無効」ではなく「無効であることを新しいauthoritative eventとして表現する」**方が構造に合う。

---

## 6. 今回まだ一般則として確定していないこと

このincidentだけから、次を普遍則としては扱わない。

- あらゆるagent systemに中央Identity Correction Registryが必須
- clean rekeyが常に最善
- immutable historyがmutable stateより常に優れている
- 特定のID schemaや命名規則が万能
- すべてのidentity conflictに人間確認が必要
- scheduled task architectureの特定構成が優れている

今回確認できたのは、**versioned durable historyと複数readerがある環境でidentity collisionが起きた場合、current-state overwriteだけでは修復が閉じない**ということと、その事故を安全に扱うための設計候補である。

---

## 7. AI Business Transformationへの適用

この知見は、AIエージェントや自動化を業務へ導入するときの「状態管理・監査・例外処理」の観点で再利用価値がある。

特に次の問いへ使える。

- AIが参照するtask identityはどこで決まるか
- retry / rerun / handoffで同じtaskと別taskをどう区別するか
- 間違った記録を監査履歴を壊さず訂正できるか
- dashboardとcanonical historyを混同していないか
- migration時にproducerだけでなくconsumerも更新したか
- ambiguity時にagentがside effectを止められるか

これは「AIエージェントを増やす」話よりも、**複数agentが同じ状態を安全に解釈できる契約を作る**話として扱う方がよい。

---

## 8. Research Meshとの境界

この文書はResearch Meshのcurrent operational stateをGitHubへ複製するものではない。

最新のQuestion ID対応、Board row、owner、receipt、scheduled task prompt、ACTIVE_POLICY等が必要な場合はResearch Mesh側のcanonical sourcesをfresh readする。

GitHub側へ残すのは、

- 再発防止に使える設計原則
- negative knowledge
- migration / correctionの完了条件
- 他のAI業務設計へ転用できる含意

だけとする。
