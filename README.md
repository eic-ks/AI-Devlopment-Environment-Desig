# AI開発環境・ワークフロー設計プロジェクト

このリポジトリは、CLAUDE.md に定義された依頼（AIを用いた開発ワークフロー・Skills・Context/RAG・Knowledge Management等の全体設計）を、**1回の長い会話ではなく複数フェーズに分けて**進めるための作業場所です。

新しいチャットを開始したら、まず **`docs/current-state.md`** と **`docs/handoff.md`** を読んでください。今どのフェーズにいて、何が決まっていて、次に何をすべきかがそこに書いてあります。CLAUDE.md を読み直して文脈を再構築する必要はありません。

## ディレクトリの役割

| ディレクトリ | 役割 | 更新頻度 |
|---|---|---|
| `docs/` | プロジェクト全体の「北極星」。目的・評価基準・ロードマップ・現在地・引継ぎメモ | フェーズの節目ごと |
| `docs/decisions/` | ADR（決定記録）。一度決めたことを覆さないための記録 | 重要な決定をした時 |
| `requests/` | 各フェーズの依頼内容（インプット）。フェーズ開始時に読む | フェーズ開始前に確定、以後基本不変 |
| `outputs/` | 各フェーズの成果物（アウトプット）。設計ドキュメント | フェーズ完了時 |
| `research/` | 成果物を作る過程で集めた外部情報・メモ（一次情報） | 随時 |
| `archive/` | 差し替えられた旧バージョンの保管場所（削除しない） | 更新時 |

## 前提条件（Phase 0 で確定・全フェーズ共通）

- 成果物の形式：**設計ドキュメントのみ**（Claude Code の実行可能な SKILL.md 雛形などは作らない）
- 想定利用シーン：**個人（ソロ開発者としての自分専用）**
- 検証パイロット：**未特定**。特定プロジェクトに寄せず、抽象的な環境設計として進める

この前提は `docs/vision.md` に理由とともに記録されている。前提を変えたい場合は `docs/decisions/` に ADR を追加してから進めること。

## フェーズ一覧

詳細は `docs/roadmap.md` を参照。

| # | フェーズ | 依頼 | 成果物置き場 | ステータス |
|---|---|---|---|---|
| 0 | 土台整備 | — | このリポジトリ構成一式 | ✅ 完了 |
| 1 | Skills設計 | `requests/001-skills.md` | `outputs/skills/` | 未着手 |
| 2 | Workflow設計 | `requests/002-workflows.md` | `outputs/workflows/` | 未着手 |
| 3 | Context/RAG設計 | `requests/003-rag.md` | `outputs/context-rag/` | 未着手 |
| 4 | Knowledge Management設計 | `requests/004-knowledge-management.md` | `outputs/knowledge-management/` | 未着手 |
| 5 | AIへの指示方法 | `requests/005-instruction-methods.md` | `outputs/instruction-methods/` | 未着手 |
| 6 | 統合アーキテクチャ提案 | `requests/006-integrated-architecture.md` | `outputs/architecture/` | 未着手 |
| 7 | 統合・ロードマップ・ベストプラクティス | `requests/007-synthesis.md` | `outputs/synthesis/` | 未着手 |

## 1フェーズの進め方（推奨）

1. 対応する `requests/00X-*.md` を読む（前提・問い・成果物定義が書いてある）
2. 必要なら `research/` に情報を追加してから着手（重複確認は `research/README.md` の手順に従う）
3. `docs/principles.md` の評価基準に沿って設計・自己レビューする
4. 成果物を `outputs/` に保存する
5. 重要な決定は `docs/decisions/` に ADR として残す
6. `docs/current-state.md` と `docs/handoff.md` を更新してフェーズを閉じる
