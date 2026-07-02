# Request 001: Skills設計

- ステータス: 未着手
- 対応するCLAUDE.md節: 1. Skills設計
- 依存: Phase 0（完了）
- 成果物置き場: `outputs/skills/`
- 関連ADR: `docs/decisions/0001-skill-granularity.md`

## 目的

再利用可能でプロジェクトに依存しないSkillsの一覧を、階層構造付きで設計する。
また、作業の中断・再開やエージェント間の引き継ぎなど「引き継ぎコンテキスト」に対処するためのSkillsやその運用ルールの考案も設計に組み込む。

## 前提（Phase 0で確定・変更しない）

- 成果物は設計ドキュメントのみ（実行可能SKILL.md雛形は作らない）
- 個人（ソロ開発者）利用が前提
- 特定プロジェクトへのパイロットは行わない

## 出発点として与えられている候補（CLAUDE.mdより）

- Codebase Analysis（プロジェクト構造把握・エントリーポイント特定・データフロー整理・依存関係分析・変更箇所分析）
- Implementation Planning（要件整理・実装ステップ分割・影響範囲分析・テスト計画）
- Documentation Update（README/CHANGELOG/AGENT.md/Context/APIドキュメント更新）
- Code Review（可読性・保守性・性能・セキュリティ・設計レビュー）
- Refactoring（Rename/Extract/Split/Cleanupなどへの細分化）

これらを前提とせず、根本から見直してよい（CLAUDE.md本文の指示）。

## 検討すべき問い

- 「リファクタリング」のようにプロジェクト依存になりがちなSkillを、どこまで抽象化すれば汎用性を保てるか
- Skillの粒度は「1動作1Skill」か「1目的1Skill（内部で複数動作）」か。判断基準は何か
- 階層構造（親Skill/子Skillのような構成）は必要か。必要ならどう表現するか
- Skillの入出力（何を受け取り何を返すか）はどこまで標準化すべきか
- どこからがSkillの責務で、どこからがWorkflow（Skillの組み合わせ）・Context（前提知識）の責務か（`docs/principles.md` の責務分離フレーム参照）
- エージェント間の「引き継ぎコンテキスト」に対処するための専用のSkill（例: Context Handoverなど）は必要か、それとも既存のドキュメント更新Skillなどに内包させるべきか

## 成果物

1. Skills一覧（階層構造付き）
2. 各Skillの責務定義（何をする/しない）
3. 汎用性を保つための設計原則（このSkill体系固有のルール）
4. `docs/decisions/0001-skill-granularity.md` を埋める

## このフェーズ開始時に確認すべきこと

現時点で不明点なし。開始時に「今使っているSkillsやプロンプトの実例が他にあるか」を一度確認するとよい（既存資産の棚卸しになるため）。

