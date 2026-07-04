# ロードマップ（フェーズ計画）

CLAUDE.md の6セクション＋成果物10点を、7つの実行フェーズに分解したもの。1フェーズ＝1回〜数回の会話を想定。

## フェーズ一覧

| # | フェーズ | CLAUDE.md対応節 | 依頼 | 成果物 | 依存 | ステータス |
|---|---|---|---|---|---|---|
| 0 | 土台整備 | — | — | このリポジトリ構成、`docs/vision.md`、`docs/principles.md` | なし | ✅ 完了（2026-07-02） |
| 1 | Skills設計 | 1. Skills設計 | `requests/001-skills.md` | `outputs/skills/` | Phase 0 | ✅ 完了（2026-07-04） |
| 2 | Workflow設計 | 2. Workflow設計 | `requests/002-workflows.md` | `outputs/workflows/` | Phase 1 | ✅ 完了（2026-07-04） |
| 3 | Context/RAG設計 | 3. Context/RAG設計 | `requests/003-rag.md` | `outputs/context-rag/` | Phase 0（Phase 1と相互参照あり） | 未着手 |
| 4 | Knowledge Management設計 | 4. Knowledge Management | `requests/004-knowledge-management.md` | `outputs/knowledge-management/` | Phase 3 | 未着手 |
| 5 | AIへの指示方法 | 5. AIへの指示方法 | `requests/005-instruction-methods.md` | `outputs/instruction-methods/` | Phase 1, 2 | 未着手 |
| 6 | 統合アーキテクチャ提案 | 6. アーキテクチャ提案 | `requests/006-integrated-architecture.md` | `outputs/architecture/` | Phase 1〜5 | 未着手 |
| 7 | 統合・ロードマップ・ベストプラクティス | 成果物5〜10 | `requests/007-synthesis.md` | `outputs/synthesis/` | Phase 1〜6 | 未着手 |

## 推奨進行順序と理由

**1 → 2 → 3 → 4 → 5 → 6 → 7**（CLAUDE.md自体の記載順）を基本線とする。

ただし以下の相互参照に注意する（＝厳密な一方向依存ではない）：

- Phase 1（Skills）とPhase 3（Context/RAG）は概念的に絡む。「Skillに何を持たせ、何をContext/RAGに逃がすか」は`docs/principles.md`の責務分離フレームで都度切り分ける。Phase 3を先にやりたくなったら順番を入れ替えて構わない。
- Phase 6（統合アーキテクチャ）とPhase 7（統合）は、Phase 1〜5の暫定結論がなくても「仮決め」で進めてよい。後でPhase 1〜5が固まった時点で差分更新する。

## フェーズ完了の定義（Definition of Done）

各フェーズは以下がすべて揃って初めて完了とする：

1. `outputs/` 配下に成果物ドキュメントがある
2. その成果物が `docs/principles.md` の該当軸で自己レビューされている（弱い軸の明記を含む）
3. 重要な決定は `docs/decisions/` にADRとして残っている（ある場合）
4. `docs/current-state.md` のステータス表を更新した
5. `docs/handoff.md` に次フェーズ向けの引継ぎを書いた

## 変更履歴

- 2026-07-04: Phase 2完了。Workflowカタログ（メタ骨格・3ゲート・W1〜W4＋組み立て規則）と設計原則W1〜W6、ADR-0007を確定。Phase 1保留の「入力欠落時の停止規約」を原則W3として解消。
- 2026-07-04: Phase 1追補。ADR-0006でADR-0003を部分改定し、全19SkillをClaude Code形式で実装（`skills/`）。
- 2026-07-04: Phase 1完了。6カテゴリ19SkillのカタログとADR-0001（粒度・階層）を確定。
- 2026-07-02: Phase 0完了。リポジトリ構成一式を整備。フェーズ5〜7を新設（元の`requests/`は1〜4のみだった）。
