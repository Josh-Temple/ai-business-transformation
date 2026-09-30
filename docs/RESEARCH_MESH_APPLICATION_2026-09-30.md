# Research Mesh成果の適用判断

確認日：2026-09-30 JST。適用先：AI Business Transformation。
開始時main：`9fe863936cd01cd0d5652b9373fc93e73de3dc4b`。Open PRなし。

## 判断

初期サイトには4つの判断とMethodの概要があるが、読者が検証報告を点検する具体的な確認表はない。記事の追加より、既存Methodから使える静的な確認表と、限定的な研究ケースの説明を組み合わせる価値が高いと判断した。

実装：`methods/evidence-to-operation.html`。ブラウザのチェックボックスと印刷用記入欄。保存や自動合否判定は行わない。確認表は本プロジェクトによる実務上の提案であり、Research Meshが有効性を検証したツールではない。

## fresh readした正本

- Research Board: https://docs.google.com/spreadsheets/d/1GTGKNZq84pMSW5kuq-EeSx6cJcAiZosDnWnn0sGouUg/edit
- Run Journal：Q026 protocol v1 freeze（22:15）、ほか対象系列の最新記録。
- Verification Journal：下表のIntegrator、Q026 Verifier（22:31）。
- Reusable Findings：Q025由来の2件。ともにPROVISIONAL。片方はNONAUTHORITATIVEも明記。

Boardはprojectionであり、採否は直接読んだIntegrator記録の範囲を優先した。作業中に到着したQ026の22:52 Integrator結果も取得した。以下はこの確認時点の採否であり、将来の状態を保証しない。

## 主張・採否・限界

|研究・記録|成立範囲|本サイトでの扱い|未成立・適用限界|
|---|---|---|---|
|Q020 / 20260928T004800JST_OPT_INTEGRATOR_Q020_VERIFIED|固定manifestと供給された記録、合成schema、protocol v2 / interface v2 / serialization v3 / implementation v2内の決定的再構成とfail-close|確認表2・3の参考根拠|manifestの権威・完全性、未供給証拠の発見、任意のJSON・実記録・他言語、本番安全性は未成立|
|Q021 / 20260928T0948JST_OPT_INTEGRATOR_Q021_VERIFIED|protocol v6 / transformer v5、固定構造化Verifier記録と8文字列prior row、指定Policy・入力集合からの非終端提案とadmission|確認表5の参考根拠|実Sheets merge、自由記述、任意集合、terminal automation、Integrator廃止、負担軽減、本番適用は未成立。より広いQ021はTESTING|
|Q023 / 20260927T084700JST_OPT_INTEGRATOR_Q023_VERIFIED|責務・未解決前提の忠実な対応付けと次の限定実験の優先付け|採用しない。読者向け確認表との関連が間接的|優れたアーキテクチャ、役割削減の品質・費用、人間負担軽減は未成立|
|Q025 / 20260930T0850JST_OPT_INTEGRATOR_Q025_HOLD|v6の実行整合性・決定的replay・内部集計は独立再現。より広い問いはTESTING|機械的整合性とレビュー配置の効果を分ける説明だけに使用|人間の品質・時間、抽出確認の十分性、未知誤りの検出、本番レビュー方針は未成立|
|Q025 / 20260930T1549JST_OPT_INTEGRATOR_Q025_INCONCLUSIVE|v10事前系列の手順違反と結果除外|限界として明示。汚染したA/B/C値は使用しない|実質的結果、再現性、人間レビュー効果は未成立|
|Q025 / 20260930T1648JST_OPT_INTEGRATOR_Q025_CLEAN_ISOLATION_FAILED|別のclean execution protocol v1は境界を確立できずFAILED-CLOSED / INCONCLUSIVE|限界として明示|現在runtimeが必ず漏えいすること、commitment/revealの不可能性、実質的A/B/C、人間負担や本番安全性は未成立|
|Q026 / 20260930T2252JST_OPT_INTEGRATOR_Q026_FAILED|protocol v1のF1-H→Pを採点の正解に埋め込む構成上の問題。実質評価なし|RAG利用条件は採用しない。未成立事項として説明|原典確認が不要・無効、重要業務でRAGだけが安全、普遍的精度閾値は未成立。より広いQ026はTESTING|

## 一次記録の識別情報

記録はLibraryの `/Studio Lab Optimization/Verification Journal/` にある。記録名は上表の識別子に `.md` を付けたもの。第三者がこの公開文書だけで実験を再実行できるとは主張しない。原記録・実験パッケージの公開は今回の範囲外。

主根拠の実装hash：

- Q020 implementation v2: `3ae1d3886305411d39f5bc2f6de0c7589fc47c38a1dc19bca175d2ac392549a8`
- Q021 protocol v6: `ef9aae2a227e439d6fe427a928dd873dcbc6aebee2502b5bb5455267325c7111`
- Q021 transformer v5: `2de00b8e24d1900fc3084585c8d162d5729ddb4cca1dc75b05be2bf599ea727b`

Run Journalで読んだ記録：`20260930T2215JST_OPT_EXPERIMENTER_Q026_PROTOCOL_V1_FREEZE.md`。Verificationで併読した記録：`20260930T2231JST_OPT_VERIFIER_Q026_FAIL.md`。

Reusable Findings（いずれも暫定）：

- `/Studio Lab Optimization/Reusable Findings/20260930T0852JST_OPT_REUSABLE_FINDING_OUTCOME_RELEVANT_EXECUTABLE_BOUNDARY_V1.md`
- `/Studio Lab Optimization/Reusable Findings/20260930T1650JST_OPT_REUSABLE_FINDING_DETERMINISTIC_BLINDING_COMMITMENT_V1.md`

チェック項目4は前者を参考にした提案。後者は評価対象を隠す条件への注意として説明するが、現在のruntimeの漏えいや暗号学的実装の必須性を主張しない。FAIL/HOLDの問いを成功した実務研究に読み替えない。

## 重複・読者価値

トップの「小さく検証する」を具体化する。完全性と再構成の正しさ、検証PASSと書込み許可を区別する点検に使う。Kaigo Rulesの未取得の現在状態や、実在組織の導入成果は事例化せず、社内規程の例は明示した架空例とする。数値的効果や最適閾値を提示しない。

## 検証と公開判断

検証：ローカルリンク・CSS参照・ページ内anchor・ID重複検査、`git diff --check`はPASS。ブラウザ検証はPlaywrightのChromium実行ファイルがなく、取得も失敗したため未実施。モバイル表示、チェック操作、印刷レイアウトはUNVERIFIED。Research Meshのファイル、Board、Policy、scheduled taskは変更していない。

deployment_decision: HOLD

deployment_reason: 公開前のレビュー用変更として提出する。構造と導線の検査は通過したが、表示・操作・印刷のブラウザ確認が未完了のため、現在の既定方針に従い公開を保留する。
