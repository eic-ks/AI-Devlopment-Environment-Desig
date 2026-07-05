# outputs/workflows/

Phase 2（`requests/002-workflows.md`）の成果物置き場。**ステータス: 完了**。

## ファイル一覧

| ファイル | 内容 |
|---|---|
| `01-workflow-catalog.md` | Workflowカタログ（W1〜W4の4テンプレート＋メタ骨格＋組み立て規則・スキップ判定）。各WorkflowのSkill編成・ゲート配置・分岐を定義 |
| `02-orchestration-principles.md` | Workflow編成の設計原則6つ（W1直列骨格・W2承認・W3停止規約・W4セッション管理・W5スキップ判定・W6一方向依存）。「検討すべき問い」5つへの回答 |

## requests/002-workflows.md「検討すべき問い」との対応

| 問い | 答えの所在 |
|---|---|
| Workflowは「固定順序のパイプライン」か「条件分岐のあるステートマシン」か | `02-orchestration-principles.md` 原則W1。直列骨格＋ゲートにのみ分岐（遷移3種に固定）。両極の破綻理由も明記 |
| どこでユーザーの承認・レビューを挟むべきか | `02-orchestration-principles.md` 原則W2。G1（計画承認）・G2（評価裁定）・G3（完了確認）の3ゲートの位置と意味。`01-workflow-catalog.md` 3章でゲート定義 |
| 同じSkillを複数のWorkflowが共有する時、Workflow定義はどこに置くべきか | `02-orchestration-principles.md` 原則W6（一方向依存）。Workflowの定義は本ディレクトリ。定義の依存方向はWorkflow→Skill（逆向き禁止） |
| Workflowの長さが長すぎて「迷子」を再発させないための工夫は何か | `02-orchestration-principles.md` 原則W4（「1セッション1ゲート区間」）・原則W3（停止規約）。`01-workflow-catalog.md` 2章（共通外枠：F系によるセッション管理） |
| Workflow自体もSkill同様に汎用テンプレートとして持つべきか、都度組み立てるか | `01-workflow-catalog.md` 1章（メタ骨格）・8章（組み立て規則）。テンプレート4本（W1〜W4）＋テンプレート外は組み立て規則で対処。両方の運用を定義 |

## Phase 2完了の定義に対する充足状況（2026-07-04時点：すべて完了）

- 成果物: 本ディレクトリの2ファイル（Workflow一覧・設計原則）
- 自己レビュー: `02-orchestration-principles.md` 末尾の10軸レビュー（弱い軸＝学習コストを自己申告済み）
- ADR: `docs/decisions/0007-workflow-model.md`（決定済み）
- 状態更新: `docs/current-state.md` / `docs/handoff.md` 更新済み
