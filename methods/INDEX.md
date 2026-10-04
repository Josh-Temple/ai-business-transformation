# Methods Index

AI Business Transformation のMethodコンテンツへ到達するための薄い索引です。

このファイルはmethod本文や現在の研究状態を複製しません。質問に合うmethodを選び、実際の内容・根拠・限界は各method本文で確認してください。

## Methods

### Evidence to Operation

- path: `methods/evidence-to-operation.html`
- use for:
  - AI/自動化の検証結果を本番業務へ適用できる範囲の確認
  - PoCの成功と本番運用許可の分離
  - 入力集合、検証範囲、異常時挙動、human approvalの確認
  - 限定的な研究結果から実務提案へ一般化するときの境界確認
- do not use as:
  - 特定組織・自治体・業界の事実の正本
  - 「チェック項目を満たせば安全」という普遍的な合格基準

## Research support records

Methodへ昇格する前のResearch Mesh由来の適用判断を、current stateとは分離したsnapshotとして記録する。

- `docs/RESEARCH_MESH_APPLICATION_2026-09-30.md`
  - Q020/Q021/Q025/Q026を中心に、初回のEvidence to Operation Methodへ何を採用・不採用にしたか。
- `docs/RESEARCH_MESH_APPLICATION_2026-10-02.md`
  - Q028/Q029、Q025+Q026のESTABLISHED reusable finding、Q030の未昇格判断、Q031のbounded verified finding。
  - PoC→組織成果、workflow redesign、evaluation boundary、skill retention、synthetic / real evidence selectionの境界を記録。
  - Q032はpre-execution段階のため、monitoring / stop / rollback一般則としては未昇格。
- `docs/RESEARCH_MESH_APPLICATION_2026-10-05.md`
  - Research Meshで実際に起きたidentity / lineage conflictから、versioned historyでの訂正、stable_id / run_id / provenanceの分離、exact-match correction、clean rekey、fail-closed、reader側更新まで含むmigration完了条件を整理。
  - current Boardやscheduled task状態は複製せず、複数AI・自動化へ再利用できる設計知見とnegative knowledgeだけを記録。

これらはResearch Meshの最新runやBoard状態の正本ではない。現在状態が必要な場合はResearch Mesh側のcanonical sourcesをfresh確認する。

## Routing rule

1. 個別組織・制度・調達・研究の事実は、そのdomain repositoryで確認する。
2. その事実を業務設計や導入判断へ一般化するときだけ、対応するMethodを使う。
3. Methodが参照する研究結果と、Method自身の実務提案を区別する。
4. Method本文に未検証・限定条件がある場合、その境界を回答でも保持する。
