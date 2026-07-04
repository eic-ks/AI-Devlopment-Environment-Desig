# outputs/skills/

Phase 1（`requests/001-skills.md`）の成果物置き場。**ステータス: 完了**。

## ファイル一覧

| ファイル | 内容 |
|---|---|
| `01-skill-catalog.md` | Skill全一覧（6カテゴリ19Skill、2層構造）と各Skillの責務定義（6項目共通フォーマット） |
| `02-design-principles.md` | この体系固有の設計原則6つ＋Skill/Workflow/Contextの責務境界の判定基準・判定例＋10軸自己レビュー |

## requests/001-skills.md「検討すべき問い」との対応

| 問い | 答えの所在 |
|---|---|
| リファクタリングSkillをどこまで抽象化すれば汎用性を保てるか | `02-design-principles.md` 原則1（注入原則）。依存するのは判断基準だけで手順は汎用、基準を前提入力に追い出す。具体形は `01-skill-catalog.md` §5（C系4Skill） |
| Skillの粒度は「1動作1Skill」か「1目的1Skill」か。判断基準は何か | `02-design-principles.md` 原則3（分割基準）。手順が違えば分割、基準・対象が違うだけならパラメータ化。粒度は「1成果物1Skill」 |
| 階層構造は必要か。必要ならどう表現するか | 必要——ただし分類として。`01-skill-catalog.md` §1.1（2層構造）と `02-design-principles.md` 原則4（階層＝分類）。実行合成はWorkflowの責務 |
| 入出力はどこまで標準化すべきか | `02-design-principles.md` 原則5（薄い標準化）。6項目の共通記述フォーマットのみ（`01-skill-catalog.md` §1.4）。例外的にF系だけ厳格テンプレート |
| Skill/Workflow/Contextの責務境界はどこか | `02-design-principles.md` 「Skill/Workflow/Contextの責務境界」節（判定の問い4つ＋判定例6つ）。「実装」をSkillにしない整理は `01-skill-catalog.md` §2.1 |
| 引継ぎ専用Skill（Context Handover等）は必要か、既存Skillに内包すべきか | 専用Skillとして独立が必要。`01-skill-catalog.md` §2.2（独立させた理由）と§8（F系3Skill：handover/checkpoint/restore） |

## Phase 1完了の定義に対する充足状況（2026-07-04時点：すべて完了）

- 成果物: 本ディレクトリの2ファイル
- 自己レビュー: `02-design-principles.md` 末尾の10軸レビュー（弱い軸＝学習コストを自己申告済み）
- ADR: `docs/decisions/0001-skill-granularity.md`（決定済み）
- 状態更新: `docs/current-state.md` / `docs/handoff.md` 更新済み
