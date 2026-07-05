# outputs/knowledge-management/

Phase 4（`requests/004-knowledge-management.md`）の成果物置き場。**ステータス: 完了**。

## ファイル一覧

| ファイル | 内容 |
|---|---|
| `00-design-plan.md` | 設計方針・骨子（G1承認済み）。KB分類体系・命名規則・重複排除・ライフサイクル等の中心判断6つを規定 |
| `01-kb-structure.md` | KB内部構造 — L4参照層の5分類・ディレクトリ構造・命名規則・記録フォーマット（定型ヘッダ＋種類別テンプレート）・検索手順 |
| `02-knowledge-lifecycle.md` | 知識のライフサイクル — 追加・取り込み・更新・失効・削除と重複排除・整合性確認の定型フロー |
| `03-phase3-boundary.md` | Phase 3との役割分担 — 規定の所在対応表と二重定義・矛盾ゼロの検証 |

## requests/004-knowledge-management.md「検討すべき問い」との対応

| 問い | 答えの所在 |
|---|---|
| 新規知識を追加する時の判断フロー（重複確認→保存場所→要約粒度）をどう定型化するか | `02-knowledge-lifecycle.md` 1〜2章（追加フロー・E3の実行手順）。重複確認はglob+grepの分散実行・全量チェックなし |
| 重複削除・矛盾発見を定期的な棚卸しWorkflowに落とし込めないか | `02-knowledge-lifecycle.md` 4章（整合性確認の定型フロー）。棚卸しトリガーはPhase 3（`../context-rag/03-maintenance-cycle.md`）が規定し、本フェーズはその上の手順を定める |
| 情報の「鮮度」をどう管理するか | `01-kb-structure.md` 3章（定型ヘッダの「更新日・ステータス」）。`02-knowledge-lifecycle.md` 3章（失効マーキング・削除の判断基準） |
| バージョン管理はファイル＋Gitで十分か | `00-design-plan.md` 判断5。Gitのみで十分と決定。`archive/` 方式（上書き前コピー）は禁止。失効マーキングまたは削除（Gitに残るため安全側）。ADR-0008に記録 |
| 検索性向上のためのファイル命名・タグ付け・インデックスはどう設計するか | `01-kb-structure.md` 2章（命名規則: ファイル名＝インデックス・検索語の含め方・汎用語禁止）・3章（定型ヘッダのタグ項目）。インデックスファイルは不保持 |

## Phase 4完了の定義に対する充足状況（2026-07-05時点：すべて完了）

- 成果物: 本ディレクトリの3ファイル（KB内部構造・ライフサイクル・Phase 3との役割分担）
- 自己レビュー: `01-kb-structure.md`・`02-knowledge-lifecycle.md` 各末尾の10軸レビュー
- ADR: `docs/decisions/0008-kb-structure.md`（決定済み）
- 状態更新: `docs/current-state.md` / `docs/handoff.md` 更新済み
