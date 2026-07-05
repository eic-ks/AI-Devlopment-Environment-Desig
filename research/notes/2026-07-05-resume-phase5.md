# 再開計画メモ（2026-07-05 セッション復元）

## 再開計画（3行以内）

1. Phase 5（AIへの指示方法）を開始する。`requests/005-instruction-methods.md` の「検討すべき問い」5つに順に答える
2. 入力は `outputs/skills/01-skill-catalog.md`・`outputs/workflows/01-workflow-catalog.md`・`02-orchestration-principles.md`（Skills/Workflowを「呼び出す指示」の観点を含めるため）
3. 成果物4点（ベストプラクティス集・タスク分割基準・コンテキスト渡し方使い分け表・レビュー依頼テンプレート）を `outputs/instruction-methods/` に保存し、`docs/current-state.md`・`docs/handoff.md` を更新する

## 根拠ファイル

- `docs/current-state.md`（今のフェーズ：Phase 4完了 → Phase 5待ち、次にやること）
- `docs/handoff.md` 最新の引継ぎ（Phase 4完了、次アクション3点）
- `requests/005-instruction-methods.md`（Phase 5の問い・成果物定義）

## 状態ファイルとの矛盾・解消済み事項

- handoff の保留「このリポジトリ自体は未コミット」→ **解消済みと判断**。git status はクリーンで、コミット `a716f84 フェーズ１〜４までの成果物を生成` が存在する

## 保留・要確認（解消済み）

- 適用作業3点の実施タイミング → ユーザー裁定（2026-07-05）：「一部だけ先にやる」。②`context/kb-format.md` の実体化のみ先行実施済み（scaffold雛形をコピー＋リポジトリ固有注記）。①CLAUDE.md軽量化・③`research/` 移行は設計フェーズ完了後に実施
