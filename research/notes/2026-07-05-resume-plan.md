# 再開計画メモ（2026-07-05 セッション開始時）

session-restore の成果物。何を根拠に何から再開するか。

## 再開計画（3行以内）

1. Phase 3（Context/RAG設計）を開始する。`requests/003-rag.md` の「検討すべき問い」5つに答える設計を行う
2. Phase 1/2 から持ち越した中心要件（固有知識の恒久的な置き場所、前提入力の注入の仕組み、原則W3停止規約の実行時強制）を Context 設計の要件に組み込む
3. 成果物（アーキテクチャ図・AGENT.md判断基準・RAG判断基準＋更新運用フロー・ADR-0002）を `outputs/context-rag/` と `docs/decisions/0002-context-architecture.md` に保存する

## 根拠ファイル

- `docs/current-state.md` — Phase 2 完了（2026-07-04）、次は Phase 3
- `docs/handoff.md` 最新の引継ぎ — 確定事項6件・保留3件・次アクション3件
- `requests/003-rag.md` — 問い5つ＋成果物4点の定義
- `outputs/skills/02-design-principles.md`（責務境界節）、`outputs/workflows/02-orchestration-principles.md`（原則W3・W6） — Phase 3 の入力（読み込み済み）

## 状態ファイルとの矛盾・不明点

- 矛盾: 該当なし
- 不明点（`requests/003-rag.md`「このフェーズ開始時に確認すべきこと」）: 2026-07-05 セッション冒頭でユーザーに確認済み
  1. 日常の AGENT.md/CLAUDE.md → **肥大化している**（規約・手順・経緯が混在して長く、何が効いているか分からない状態）
  2. RAG 基盤（Vector DB 等） → **未導入・まっさら**。導入すべきかどうか自体をこのフェーズでゼロから検討する
