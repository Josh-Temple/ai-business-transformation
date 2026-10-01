# Research Mesh transferable findings — 2026-10-02

確認日：2026-10-02 JST
適用先：AI Business Transformation
性格：research support record / snapshot。Research Meshの現在状態そのものの正本ではない。

## 1. この記録の目的

Research Meshで得られた成果のうち、AI導入・BPR・評価設計の判断に再利用する価値があり、GitHubへ残す意味があるものだけを抽出する。

次は記録しない。

- scheduled taskの最新run時刻や現在のownerなど、高頻度に変わる運用状態
- Research Boardのprojectionをそのまま複製した一覧
- 未検証の仮説を確定知見として昇格したもの
- internal Library receiptの全文

採用基準は、独立Verifier / Integratorで限定的に成立した知見、または「何がまだ成立していないか」という実務上重要なnegative knowledgeである。

---

## 2. Q029 — PoC・局所的なAI効果を組織成果へ外挿しない

status: **BOUNDED VERIFIED**

Research Meshで成立した範囲では、短期のtask-levelな生成AI効果が、より広いservice / workforce outcomeへ移る可能性は、少なくとも次の条件と関係する。

- pilotと本番でtask / populationが大きくずれていない
- ordinary useが実際に起きている
- speedだけでなくquality / service outcomeも改善している
- review / coordination burdenが大きく増えていない
- 節約されたcapacityを組織が実際に回収・再配分できる
- 観測期間が、評価したい成果の発現まで十分かを分けて考える

一方、個人が処理時間を短縮しても、meetingやcoordination-heavy workが変わらない、追加のoversight / integration workが発生する、またはsaved capacityが回収されない場合、より広い成果は弱まる、または観測期間内ではnullになり得る。

この知見は、**「PoCで生産性が上がった = ROIが出る」ではない**ことを示す判断材料として使える。

### 主な外部根拠

- Brynjolfsson, Li & Raymond, Generative AI at Work
  https://www.nber.org/papers/w31161
- Dillon, Jaffe, Immorlica & Stanton, Shifting Work Patterns with Generative AI
  https://www.microsoft.com/en-us/research/publication/shifting-work-patterns-with-generative-ai/
- Humlum & Vestergaard, Still Waters, Rapid Currents
  https://www.nber.org/papers/w33777
- Farach et al., human-AI collaboration field experiment
  https://www.microsoft.com/en-us/research/publication/human-ai-collaboration-field-experiment/
- Dell'Acqua et al., The Cybernetic Teammate
  https://www.nber.org/papers/w33641

### 未成立

- 普遍的なpilot-to-ROI変換則
- 数値的なROI / staffing / review / adoption threshold
- finite-horizonのnullから恒久的な無価値を推論すること
- 全業種への一般化
- workflow redesignが一般に必要という結論

実務上は、PoC評価を「task productivity」だけで閉じず、service / quality / workforce / coordination / capacity captureまで分けて見る方が安全である。

---

## 3. Q028 — 「AIを入れるなら業務再設計が必要」はまだ一般則ではない

status: **BOUNDED INCONCLUSIVE**

現在の高品質な根拠では、次のどちらも一般則としては成立していない。

- AI導入ではmaterial workflow redesignが一般に必要・優越する
- 既存workflowへAI支援を差し込むだけで一般に十分である

重要なのは、**再設計の必要性を前提にしないこと**である。

Research Meshでは、customer supportやsoftware developmentなどで、既存workflowへのassistive insertionだけでも有意なtask-level gainが出る事例を確認した。一方、同じAI toolの周辺へ追加したcollaboration / scaffoldingが、特定の条件では品質や生産量を悪化させる反例もあった。

ただし、AI capabilityを概ね固定したまま、

- A: assistive insertion
- B: 明示的なworkflow/process redesign

を比較し、end-to-end process outcomeとredesign burdenを同時に測った十分強いfield evidenceは確認できていない。

したがって現時点では、BPRを「AI導入の前提条件」にするより、

> task-localな支援でどこまで改善するかを確認し、handoff・coordination・review・役割分担がボトルネックとして残る場合に、再設計仮説を追加で検証する

という扱いが適切である。

### 未成立

- workflow redesignの一般的な必要性・優越性
- assistive insertionの一般的な十分性
- redesignの普遍的な費用対効果
- coordination complexity等から導く万能threshold

このINCONCLUSIVEは失敗ではなく、**「AI導入 = BPR必須」と断定しないためのnegative knowledge**として価値がある。

---

## 4. Q025 + Q026 — 評価結果を証拠として扱うなら、結果を左右する境界をend-to-endで固定する

status: **ESTABLISHED reusable methodological finding**

2026-09-30時点では暫定だったが、独立したQ025・Q026の失敗系列から同じ問題が確認され、Reusable Finding v2ではESTABLISHEDへ上がった。

再利用可能な原則は次のとおり。

> source/input生成から最終結果までの間に、schema mapping、adapter、authority/currentness/scope判定、validation、sampling/review-touch、scoring、summary serializationなど、outcomeを変え得る自由度が残るなら、その境界全体をfreeze / identifyしてからでないと、replayやbenchmark結果を強い証拠として扱えない。

component codeやsource bytesだけを固定しても不十分な場合がある。途中の意味付けやqualification ruleが未固定なら、同じ入力から別のPASS/FAILを作れてしまうためである。

### AI Business Transformationへの含意

PoCやbenchmarkのレビューでは、単に「モデル・prompt・test dataが固定されているか」ではなく、

- input変換
- source authority / currentness判定
- scope mapping
- validator
- sampling
- human review touch
- score
- summary

まで、**結論を変え得る箇所が事前に特定されているか**を確認する。

これは既存Method methods/evidence-to-operation.html の「結果を左右する処理が固定されているか」を、より強い根拠で支える。

### 未成立

- あらゆる実装詳細を固定すべきという主張
- この原則だけで本番安全性が証明されること
- どのsemantic fieldがoutcome-relevantかを自動判定できること

---

## 5. Q025 — deterministicなblind evaluationでは「隠す」だけでなくprecommitが必要になり得る

status: **PROVISIONAL**

deterministic generatorをreviewerが読める場合、realized evaluation rowsそのものを隠しても、seedやrealization entropyが見える・導出可能なら、reviewerが評価対象を再構成できる。

逆にentropyをexecutorだけが自由に選べると、review後のreroll / selectionが可能になる。

この2つを同時に避ける設計候補は、

1. review前に将来のrealizationを1つへprecommitする
2. concrete entropyはreviewerから隠す
3. reveal後にcommitmentとの一致を検証する

という形である。

ただし、この知見は1つのQ025 lineageに基づく **PROVISIONAL** であり、暗号学的commitmentが常に必須、現在runtimeが実際に漏洩する、といった一般化はしない。

---

## 6. Q030 — skill retentionは有望なテーマだが、まだ公開知見へ昇格しない

status: **OPEN / NOT PROMOTED**

Q030は「短期生産性と、人間の技能習得・維持をどう両立するか」を扱う。

現段階で価値がある設計上の区別は、

- AI-assisted performance
- AIを外した後のlater unaided capability

を別outcomeとして測ること。

また、単なる「AI利用あり/なし」や利用頻度だけでなく、

- answer / delegation-heavy use
- cognitively engaged / scaffolded use

の違いを見る方向が検討されている。

しかし、職場・専門業務でA vs Bを十分に識別し、assisted performanceとlater unaided capabilityを同時に測る直接因果Evidenceはまだ不足している。したがって現時点では、

- 「AIはdeskillingを起こす」
- 「scaffoldingすれば技能は守られる」
- 「このtaskはAIへ委ねてよい」

という一般則へ昇格しない。

今後、独立Verifier / Integratorでbounded resultが閉じた後に、必要なら別の公開Research Note / Methodへ昇格する。

---

## 7. この時点でのGitHub側の扱い

### すぐ再利用してよい

1. **PoCのtask-level gainと組織成果を分ける**
   Q029のbounded verified findingを、PoC→本番判断、KPI、ROI記事の根拠候補にする。

2. **workflow redesignを最初から正解扱いしない**
   Q028のbounded inconclusiveを、AI導入時のBPR設計での反証材料として使う。

3. **evaluation boundaryをend-to-endで固定する**
   Q025/Q026のESTABLISHED reusable findingを、Evidence to Operation Methodの根拠更新候補にする。

### まだ昇格しない

- Q030のskill retention一般則
- universal human-review allocation rule
- RAGの普遍的な原典確認省略条件
- workflow redesignの数値threshold
- pilot-to-ROIの数値threshold

---

## 8. Research Meshとの境界

この文書はResearch Meshのoperational stateをGitHubへ複製するものではない。

current owner、latest run、Board projection、ACTIVE_POLICY、scheduled task状態などは、引き続きResearch Mesh側の正本をfresh readする。

GitHubへ残すのは、時間が経っても再利用価値のある、

- bounded finding
- negative knowledge
- research-design rule
- public-facing contentへ昇格する前の適用判断

だけとする。
