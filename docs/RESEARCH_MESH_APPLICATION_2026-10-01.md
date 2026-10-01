# Research Mesh成果の適用判断 — 2026-10-01

確認日：2026-10-01 JST。適用先：AI Business Transformation。

## 今回の判断

Research MeshのQ028は、生成AI導入時の「既存workflowへのAI支援追加」と「AI導入に伴う明示的なworkflow/process redesign」を比較する証拠整理を行った。

独立VerifierとIntegratorが確認したbounded resultは `INCONCLUSIVE` である。現在採用された証拠からは、workflow redesignが一般に必要・優越とも、一般に有害・不要とも結論できない。既存workflowへのassistive insertionだけでboundedなtask/throughput改善が生じる例がある一方、process redesignの追加効果を、AI能力や導入強度、training、staffing等のco-interventionから分離して示す十分な比較証拠は得られていない。

このため、サイトの基本姿勢を「AI導入前には原則として業務再設計が必要」と読める表現にはしない。代わりに、AI支援による局所的な改善が工程全体へ伝わるかを確認し、引継ぎ・レビュー・例外処理などにボトルネックが残る場合に、具体的な再設計案を比較検証する、という条件付きの表現へ修正する。

## 反映した変更

対象：`index.html` の Decision Focus 02。

変更前：

> 例外だらけの業務をそのまま自動化せず、標準化・入力設計・責任分界を先に整える。

変更後：

> AI支援だけで成果が工程全体へ届くかを確かめ、引継ぎ・レビュー・例外処理がボトルネックなら、具体的な業務再設計を比較検証する。

Heroの「AIを入れる前に、業務を設計する」は変更しない。「業務を設計する」は、必ず大規模な業務再設計を先行させるという意味ではなく、適用範囲・人間確認・失敗時運用・評価条件を設計するという本Repository全体の位置づけとして維持する。

## Q028の根拠と限界

主要なdurable receipt：

- `/Studio Lab Optimization/Verification Journal/20261001T1749JST_OPT_INTEGRATOR_Q028_INCONCLUSIVE.md`
- `/Studio Lab Optimization/Verification Journal/20261001T1734JST_OPT_VERIFIER_Q028_PASS.md`
- `/Studio Lab Optimization/Run Journal/20261001T1716JST_OPT_EXPERIMENTER_Q028_INCONCLUSIVE.md`

成立していないこと：

- workflow redesignが一般に必要または優越であること
- workflow redesignが一般に有害または不要であること
- assistive insertionが一般に十分であること
- 組織横断で使えるB-over-Aの因果効果
- coordination、handoff、complexity、riskに関する普遍的閾値
- 公共部門・規制業務への直接転用
- end-to-endのredesign cost-benefit

したがって今回のサイト変更は、Q028から新しい一般則を追加するものではなく、既存の強い表現をResearch Meshの現在の証拠範囲へ戻す修正である。

## Q029の扱い

Q029は、短期pilotで観測された個人・task-levelの生産性向上を、継続的な組織ROIやservice-level改善へどこまで外挿できるかを研究している。

2026-10-01時点で、protocol v1に対するScout/Criticの独立攻撃は `SUPPORT_WITH_LIMITS`。少なくとも次の修正が必要とされている。

- realization horizon / outcome lagを独立した評価軸または主要moderatorとして扱う
- adoption / denominator evidenceを `BOUNDARY_ONLY` としてoutcome-path evidenceから分ける
- evidence hierarchyをclaim-specificに扱う
- positive/negative case balanceを証拠の重み付けではなくsearch/stop ruleとして扱う

主要なdurable receipt：

- `/Studio Lab Optimization/Run Journal/20261001T2016JST_OPT_EXPERIMENTER_Q029_PROTOCOL_FREEZE.md`
- `/Studio Lab Optimization/Run Journal/20261001T2026JST_OPT_SCOUT_CRITIC_Q029_PROTOCOL_COUNTEREVIDENCE.md`

現時点ではsubstantiveなpilot-to-ROI transfer rule、普遍的なadoption率・期間・task share・review burden・ROI閾値は成立していない。そのためQ029を根拠とする公開Methodや確定的なサイト本文は今回追加しない。

次に反映を検討するのは、protocol v2、substantive synthesis、独立検証、Integratorのbounded conclusionまで進んだ後とする。

## 検証と公開判断

今回の公開本文変更は1文のみで、Q028のbounded INCONCLUSIVEに合わせて断定を弱めるもの。Q029の未確定結果は公開本文へ採用していない。

deployment_decision: HOLD

deployment_reason: Repositoryへの研究反映は行うが、今回はResearch Meshとの整合修正と内部の適用記録が中心であり、この変更単独で手動production releaseを行う必要性は低い。既定のDeployment Policyに従い公開は保留する。
