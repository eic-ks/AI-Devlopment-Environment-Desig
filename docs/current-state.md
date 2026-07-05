# 現在地（Single Source of Truth）

**新しいチャットではまずこのファイルを読む。** CLAUDE.mdやこれまでの会話履歴を遡って再構築する必要はない。

## 今のフェーズ

**Phase 3（Context/RAG設計）完了（2026-07-05） → Phase 4（Knowledge Management設計）待ち**

## 確定済みの決定事項

| 決定 | 内容 | 記録場所 |
|---|---|---|
| 成果物形式 | 設計ドキュメント基本。Phase 1のSkillsのみClaude Code形式で実装済み（`skills/`） | `docs/decisions/0003-deliverable-format.md`、`0006-build-executable-skills.md` |
| 利用シーン | 個人（ソロ開発者専用） | `docs/decisions/0004-target-user.md` |
| パイロット対象 | 未特定、抽象的な環境設計として進める | `docs/decisions/0005-no-pilot-project.md` |
| フェーズ分割 | CLAUDE.mdの6節＋成果物10点を7フェーズに分解 | `docs/roadmap.md` |
| 評価基準 | 10軸（汎用性〜導入コスト）＋責務分離フレーム | `docs/principles.md` |
| Skillの粒度・階層 | 「1成果物1Skill」＋分割基準「手順が違えば分割、基準が違うだけならパラメータ化」。階層は2層の分類のみ（実行階層は禁止） | `docs/decisions/0001-skill-granularity.md` |
| Skill体系 | 6カテゴリ19Skill（理解/計画/変換/評価/記録/セッション管理）＋設計原則6つ | `outputs/skills/01-skill-catalog.md`、`02-design-principles.md` |
| 実行可能Skillの構築 | ADR-0003を部分改定し、全19SkillをClaude Code形式で実装（`skills/`、`~/.claude/skills/`へsymlink済み） | `docs/decisions/0006-build-executable-skills.md`、`skills/README.md` |
| Workflowモデル | 直列メタ骨格＋限定ゲート分岐（3ゲート・遷移3種固定）。承認はG1計画承認/G2評価裁定/G3完了確認のみ。テンプレート4本（W1〜W4）＋組み立て規則のハイブリッド | `docs/decisions/0007-workflow-model.md`、`outputs/workflows/01-workflow-catalog.md`、`02-orchestration-principles.md` |
| 入力欠落時の停止規約 | Workflowの各ステップ開始条件＝Skill前提入力【必須】の充足確認。欠落時は停止して要求、推測補完禁止（Phase 1保留事項の解消） | `outputs/workflows/02-orchestration-principles.md` 原則W3 |
| Context/RAGアーキテクチャ | 読み込みタイミングで5層配置（L1常駐/L2状態/L3注入/L4参照/L5定義）。固有知識の恒久的な置き場＝L3。L1は3テスト＋分量予算150行、L3/L4は「従うもの/引くもの」で判定。Vector DB不採用（ファイルベースKB＋エージェント検索、再検討条件付き）。圧縮は構造化のみ・要約禁止。W3強制＝L1常駐規約＋`context/INDEX.md`＋存在判定（Phase 2保留事項の解消） | `docs/decisions/0002-context-architecture.md`、`outputs/context-rag/00〜03` |

## 未解決・要確認事項

- このリポジトリのCLAUDE.mdへの適用（`outputs/context-rag/02-placement-criteria.md` 5章で判定済み・追い出し3点＋roadmap二重記載の解消）は未実施。実施タイミングをユーザーに確認する
- KB（L4）内部の分類体系・記録フォーマット・検索性の詳細設計 → **Phase 4の中心**
- 昇格の回数集計・降格の参照検出・棚卸し周期の計測の仕組み → Phase 7（運用設計）
- Workflow・Context体系の実行可能形式（コマンド化・AGENT.md雛形等）での実装は未決定。現時点は設計ドキュメントのみ

## 次にやること

1. `requests/004-knowledge-management.md` を読む
2. `outputs/context-rag/01-context-architecture.md`（L4の定義・書き込み経路）と `03-maintenance-cycle.md`（書き込み規律・検索方式）を入力に、Knowledge Management設計を議論し、`outputs/knowledge-management/` に成果物を保存する
3. 完了したらこのファイルと `docs/handoff.md` を更新する

## 更新ルール

- フェーズが1つ進むたびに「今のフェーズ」「確定済みの決定事項」「次にやること」を書き換える
- 過去の状態を残したい場合は書き換えず `archive/` に日付付きでコピーしてから更新する
- このファイルは常に現在時点の状態のみを反映する（変更履歴は `docs/roadmap.md` 側に置く）
