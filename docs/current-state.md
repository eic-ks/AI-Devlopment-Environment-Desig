# 現在地（Single Source of Truth）

**新しいチャットではまずこのファイルを読む。** CLAUDE.mdやこれまでの会話履歴を遡って再構築する必要はない。

## 今のフェーズ

**Phase 2（Workflow設計）完了（2026-07-04） → Phase 3（Context/RAG設計）待ち**

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

## 未解決・要確認事項

- 停止規約（原則W3）の実行時強制の仕掛けと、固有知識（観点リスト・規約・テンプレート等）の恒久的な置き場所 → **Phase 3の中心要件**
- ゲート形骸化の検出・「3回ルール」の計測・テンプレート見直し周期 → Phase 7（運用設計）
- Workflowの実行可能形式（コマンド化等）での実装は未決定。現時点は設計ドキュメントのみ

## 次にやること

1. `requests/003-rag.md` を読む
2. `outputs/skills/02-design-principles.md`（責務境界）と `outputs/workflows/02-orchestration-principles.md`（原則W3・W6）を入力に、Context/RAG設計を議論し、`outputs/context-rag/` に成果物を保存する
3. 完了したらこのファイルと `docs/handoff.md` を更新する

## 更新ルール

- フェーズが1つ進むたびに「今のフェーズ」「確定済みの決定事項」「次にやること」を書き換える
- 過去の状態を残したい場合は書き換えず `archive/` に日付付きでコピーしてから更新する
- このファイルは常に現在時点の状態のみを反映する（変更履歴は `docs/roadmap.md` 側に置く）
