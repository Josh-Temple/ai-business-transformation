# HANDOFF — Portfolio Pilot / AI Business Transformation

Updated: 2026-09-29 JST  
Repository: `Josh-Temple/ai-business-transformation`  
Purpose: 次セッションで、Research Meshの内部改善ループからPortfolioの実戦構築へ移行した状態を、そのまま継続できるようにする。

---

## 1. このセッションで決めたこと

Research Meshは、内部プロトコル改善そのものを研究し続ける段階から、実際の外部テーマへ投入して受入試験する段階へ移す。

最初の実戦投入先は、転職用に検討している4サイトのうち `AI Business Transformation` とする。

4サイトの役割は次の整理を維持する。

- AI Business Transformation — Consulting / Thinking
- Kaigo Rules — Domain / Operations
- Parenting Evidence — Research / Evidence
- Studio Lab Research — AI Engineering / Experimentation

4サイトを一度に作るのではなく、active themeは原則1サイトずつ進める。最初はAI Business Transformationを中心にし、他サイトをケーススタディや実績の根拠として接続する。

---

## 2. AI Business Transformation の現在位置

### Repository

`Josh-Temple/ai-business-transformation`

2026-09-29 08:37 JST時点でfresh確認した `main`:

`1206601b24a5573eeb32b72316458505a515a707`

このSHAはPR #2のmerge commit。

### 既存の正本ドキュメント

- `README.md`
- `docs/PROJECT_CONCEPT.md`
- `docs/AUDIENCE_POSITIONING.md`
- `docs/DEPLOYMENT_POLICY.md`
- `AGENTS.md`
- `vercel.json`

次セッションでは、過去チャットではなく必ずmainをfresh readしてから作業すること。

---

## 3. サイト初期実装

PR #1で初期サイトを実装・merge済み。

PR:
https://github.com/Josh-Temple/ai-business-transformation/pull/1

初期実装ファイル:

- `index.html`
- `styles.css`

デザイン方針:

- Baukasten系
- オフ白背景
- 濃紺タイポグラフィ
- くすみ赤・青・黄を限定的に使用
- 広い余白
- 強い見出し階層
- カードUIを避ける
- 罫線とタイポグラフィ中心
- Androidスマートフォンでも読めるレスポンシブ構成

トップメッセージ:

> AIを入れる前に、業務を設計する。

現在の主要セクション:

- Positioning
- Decision Focus
- Method
- Selected Cases
- About

Decision Focusでは次の4判断を前面に出している。

1. どの業務にAIを使うか
2. 先に業務を再設計すべきか
3. 何を人間に残すか
4. 何を成果として測るか

Selected Casesでは現在以下を接続している。

- Kaigo Rules
- Studio Lab Research

---

## 4. 現在の公開サイト

Vercel project:

`ai-business-transformation`

Production URL:

https://ai-business-transformation-nine.vercel.app

2026-09-29の確認時点でHTTP 200 / READY。

現在Productionが指しているGitHub commit:

`a05d7d5c54a21c99c1caa1884650d3a01621992a`

これはPR #1をmergeした時点のサイト初期版。

現在のmainはこれより先の `1206601b...` だが、PR #2は運用設定のみで、Productionは更新していない。

---

## 5. デプロイ運用 — 重要

PR #2で自動デプロイを停止した。

PR:
https://github.com/Josh-Temple/ai-business-transformation/pull/2

`vercel.json`:

```json
{
  "$schema": "https://openapi.vercel.sh/vercel.json",
  "git": {
    "deploymentEnabled": false
  }
}
```

Git push / merge をしただけではVercelへ自動デプロイしない。

基本運用:

```
作業・調査
→ commit / PR / merge
→ deployment_decision
→ HOLD が標準
→ 公開価値がまとまったときだけ DEPLOY
→ 手動Production deploy
→ READY確認
→ 公開URL確認
```

### deployment_decision

公開サイトへ影響するtaskでは、終了時に必ず以下のどちらかを判断する。

```
deployment_decision: DEPLOY
deployment_reason: ...
```

または

```
deployment_decision: HOLD
deployment_reason: ...
```

デフォルトは `HOLD`。

### DEPLOY条件

以下をすべて満たす場合に限りDEPLOYを検討する。

1. 公開サイトが実質的に改善される
2. task scopeが一つの公開状態として完結している
3. 変更範囲に既知のWIP、壊れた主要導線、明らかな仮文言がない
4. 公開対象のexact main SHAが特定できる
5. deploy後にProductionを確認できる

単にcommitやmergeが発生したことはdeploy理由にしない。

---

## 6. 次に取り掛かる内容

最優先は、トップページの装飾を増やすことではなく、最初の実質的なCase Studyを完成させること。

第一候補:

### Kaigo Rules Case Study

仮テーマ:

> 複雑な制度文書をAIで扱うとき、正確性をどう担保するか

狙い:

- 単なる開発紹介にしない
- 一次資料
- 変更履歴
- AI出力
- 独立検証
- human review
- UNKNOWN / HOLD
- 後続改正への追随

などを、企業・自治体のAI導入でも使える判断基準へ一般化する。

想定する読者:

- DX / AI推進担当
- 業務改革担当
- 制度・規制・品質制約の強い業務を持つ管理職
- PoCから本番運用へ移す責任を持つ人

Case Studyは、成功談よりも「どこが壊れたか」「何を人間に残したか」「何を機械検証したか」「どこで止めたか」を中心にする。

---

## 7. サイトの位置づけ

このサイトは一般的なAIメディアではない。

避ける:

- AIニュース要約
- ツール一覧
- プロンプト集
- 一般的なAI用語解説
- 根拠の薄い成功事例
- AI生成調査文のほぼそのままの公開

目指す:

```
実務で起きた問題
→ 当時の対応
→ 外部一次資料 / 研究 / 事例
→ 反証・比較
→ 現在ならどう設計するか
→ 適用条件・失敗条件
→ 他組織でも使える判断基準
```

転職ポートフォリオとしては、

> 複雑な業務を調査・分解し、AI / 従来型自動化 / 人間を組み合わせ、運用・検証まで実装できる

ことを示す。

「Webサイトを作れる」こと自体を中心価値にしない。

---

## 8. Research Mesh との関係

今回のPortfolio Pilotは、Research Mesh v1の実戦受入試験も兼ねる。

観察したい点:

- 外部テーマで良い研究問いを作れるか
- Critic / Verifierが実際に品質を上げるか
- 人間が逐次指示しなくても成果物へ収束するか
- Research Mesh自身の内部改善へ脱線しないか
- durable evidenceから状態を復元できるか
- Board projectionが遅れても誤昇格しないか
- 無限retryを避けられるか

「Research Mesh自身の研究」を長く続けることは、今後の主要目的ではない。

---

## 9. Research Mesh 最新checkpoint

重要: 次セッションでは必ずLibrary / Research Board / ACTIVE_POLICYをfresh readすること。以下は引き継ぎ作成時点の観測であり、現在状態として盲信しない。

2026-09-29 08:37 JSTまでに確認した最新系列:

- V1 retry policy — FAILED-CLOSED
- V2 — FAILED
- V3 — FAILED-CLOSED
- V4 — 08:12 Experimenter proposal
- V4 — 08:25 Scout/Critic counterevidence
- V4 — 08:31 Verifier FAIL

V4ではV3の因果順序問題を修正し、

`INTENT / RESERVATION → provider attempt → OUTCOME`

というtwo-phase append-only設計を採用した。

ただしVerifierは、durable historyに3 INTENT存在しても、bounded Library readが1件を黙って取りこぼすと `consumed_count=2` と誤復元でき、probe 4を許す可能性があるとしてFAILした。

V4の問題は、個々のreceipt identityではなく「再構築入力集合が完全であることをどう証明するか」。

必要なら次候補は、

- authoritative manifest
- frontier / sequence
- expected count
- completeness token
- omissionを検知できるclosed input boundary

などを明示する必要がある。

ただし、ここをV5, V6と延々掘ることの限界効用は下がっている。

Portfolio実戦投入を優先し、Q024はbounded HOLDに寄せる方針を強く検討する。

### Q024で維持すべき既知状態

- fresh expected-SHA pathは実行実績あり
- competing successor C / S2 は保持
- stale expected-SHA decisive provider semanticsは未確定
- stale-Dはplatform gateで複数回provider到達前にblocked
- blind retryしない
- Git canonical migrationをこの未確定状態から進めない

---

## 10. Research Meshで維持する安全境界

当面変更しない。

- Independent Verifier責務
- Integratorの最終昇格権限
- immutable receipts
- Library history
- Policy version + ACTIVE pointer分離
- fail-closed
- UNKNOWN / HOLD
- rollback / auditability
- production / permission / OAuth / secrets / schedules等のhuman boundary

簡素化する場合は、最初に

- deterministic state reconstruction
- Board projection
- retry admission
- routing
- unnecessary periodic launches

から検討する。

Verifierを消すことを最初の簡素化対象にしない。

---

## 11. 次セッションの開始手順

### Portfolioを進める場合

最初にfresh read:

1. GitHub `main` SHA
2. `AGENTS.md`
3. `docs/DEPLOYMENT_POLICY.md`
4. `docs/PROJECT_CONCEPT.md`
5. `docs/AUDIENCE_POSITIONING.md`
6. `index.html`
7. `styles.css`
8. open PR

その後、最初のCase Studyに着手する。

推奨順:

```
Kaigo Rulesのfresh state確認
→ 公開可能な実例の抽出
→ 外部一次資料・研究による一般化
→ counterargument / failure mode
→ Case Study原稿
→ Webページ実装
→ 表示検証
→ deployment_decision
```

### Research Meshを確認する場合

過去チャット・この文書のstatusを現在状態としない。

fresh read:

- Research Board
- Agent Operating Packet
- ACTIVE_POLICY
- Run Journal最新
- Verification Journal最新
- Decision Journal最新
- Q024の最新proposal / verifier / integrator lineage

V4 Verifier FAILの後にIntegrator receiptが出ている可能性があるため、必ず確認する。

---

## 12. 次セッション向け短い指示文

必要なら以下で再開できる。

> `Josh-Temple/ai-business-transformation` の作業を続けてください。最初にmain、AGENTS.md、docs/DEPLOYMENT_POLICY.md、docs/PROJECT_CONCEPT.md、docs/AUDIENCE_POSITIONING.md、現在のopen PRをfresh readしてください。過去チャットや引き継ぎ資料のSHA・statusを現在状態の根拠にしないでください。次は最初の旗艦Case Studyとして、Kaigo Rulesを題材に「複雑な制度文書をAIで扱うとき、正確性をどう担保するか」を、他組織にも使える判断基準へ一般化する作業から進めてください。公開サイトへの自動デプロイは禁止されているため、各task終了時にdeployment_decision: DEPLOY / HOLDを明示し、DEPLOYが妥当なときだけ手動Production deployしてください。

---

## 13. この引き継ぎ作成時のdeployment判定

`deployment_decision: HOLD`

理由:

この文書は内部運用・引き継ぎ用であり、公開サイトのユーザー向け内容を改善する変更ではない。Productionは更新しない。
