# outputs/context-rag/

Phase 3（`requests/003-rag.md`）の成果物置き場。**ステータス: 完了**。

## ファイル一覧

| ファイル | 内容 |
|---|---|
| `00-design-plan.md` | 設計方針・骨子（G1承認済み）。5層配置モデル・AGENT.md基準・圧縮方式等の中心判断6つを規定 |
| `01-context-architecture.md` | Context/RAGアーキテクチャ — 5層配置モデルの定義（L1常駐〜L5定義）。読み込みタイミング・参照方向・W3強制の仕掛け |
| `02-placement-criteria.md` | 配置基準 — L1残留の3テスト＋分量予算・L3/L4の判定基準・判定例・このリポジトリのCLAUDE.mdのリファレンス実装判定・圧縮方式規定 |
| `03-maintenance-cycle.md` | メンテナンスサイクル — 書き込み規律・昇格降格・棚卸し・鮮度管理・Vector DB不採用の運用上の帰結 |

## requests/003-rag.md「検討すべき問い」との対応

| 問い | 答えの所在 |
|---|---|
| 何をAGENT.mdへ残すべきか | `02-placement-criteria.md` 1章（3テスト: T1常時性・T2誤動作防止・T3他層不適合）＋2章（分量予算150行）。リファレンス実装判定は同3章 |
| 何をRAGへ入れるべきか。入れる基準は何か | `02-placement-criteria.md` 4章（L3/L4の判定基準: 「従うもの」→L3・「引くもの」→L4）。判定例15件を掲載 |
| コンテキスト圧縮はどう行うか（要約 vs 構造化） | `02-placement-criteria.md` 6章。構造化のみ許容・要約禁止（3欠陥: 取捨選択の裁量・非可逆・劣化検出不能）。適用例と免除条件も明記 |
| 長期運用でAGENT.md/RAGが肥大化・陳腐化しないメンテナンスサイクルは | `03-maintenance-cycle.md` 全体。トリガー駆動（予算超過・G3到達・矛盾発見）の棚卸し・昇格降格・鮮度義務 |
| Vector DBのような重い基盤は本当に必要か | `00-design-plan.md` 判断6・`02-placement-criteria.md` 5章。Vector DB不採用（ADR-0002）。ファイルベースKB＋エージェント検索で十分と判断、再検討条件3つを明示 |

## Phase 3完了の定義に対する充足状況（2026-07-05時点：すべて完了）

- 成果物: 本ディレクトリの3ファイル（アーキテクチャ・配置基準・メンテナンスサイクル）
- 自己レビュー: `01-context-architecture.md`・`02-placement-criteria.md`・`03-maintenance-cycle.md` 各末尾の10軸レビュー
- ADR: `docs/decisions/0002-context-architecture.md`（決定済み）
- 状態更新: `docs/current-state.md` / `docs/handoff.md` 更新済み
