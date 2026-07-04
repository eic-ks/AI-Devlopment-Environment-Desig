# 現在地（Single Source of Truth）

**新しいチャットではまずこのファイルを読む。** CLAUDE.mdやこれまでの会話履歴を遡って再構築する必要はない。

## 今のフェーズ

**Phase 1（Skills設計）完了（2026-07-04） → Phase 2（Workflow設計）待ち**

## 確定済みの決定事項

| 決定 | 内容 | 記録場所 |
|---|---|---|
| 成果物形式 | 設計ドキュメントのみ（実行可能SKILL.md雛形は作らない） | `docs/decisions/0003-deliverable-format.md` |
| 利用シーン | 個人（ソロ開発者専用） | `docs/decisions/0004-target-user.md` |
| パイロット対象 | 未特定、抽象的な環境設計として進める | `docs/decisions/0005-no-pilot-project.md` |
| フェーズ分割 | CLAUDE.mdの6節＋成果物10点を7フェーズに分解 | `docs/roadmap.md` |
| 評価基準 | 10軸（汎用性〜導入コスト）＋責務分離フレーム | `docs/principles.md` |
| Skillの粒度・階層 | 「1成果物1Skill」＋分割基準「手順が違えば分割、基準が違うだけならパラメータ化」。階層は2層の分類のみ（実行階層は禁止） | `docs/decisions/0001-skill-granularity.md` |
| Skill体系 | 6カテゴリ19Skill（理解/計画/変換/評価/記録/セッション管理）＋設計原則6つ | `outputs/skills/01-skill-catalog.md`、`02-design-principles.md` |
| 実行可能Skillの構築 | ADR-0003を部分改定し、全19SkillをClaude Code形式で実装（`skills/`、`~/.claude/skills/`へsymlink済み） | `docs/decisions/0006-build-executable-skills.md`、`skills/README.md` |

## 未解決・要確認事項

- 「前提入力の欠落時に進めずに要求する」停止規約の設計はPhase 2（Workflow）またはPhase 3（Context）に持ち越し（`docs/handoff.md` の保留事項参照）

## 次にやること

1. `requests/002-workflows.md` を読む
2. `outputs/skills/01-skill-catalog.md`（19Skill一覧）を入力に、Workflow設計（シナリオ別の組み合わせ・承認ポイント）を議論し、`outputs/workflows/` に成果物を保存する
3. 完了したらこのファイルと `docs/handoff.md` を更新する

## 更新ルール

- フェーズが1つ進むたびに「今のフェーズ」「確定済みの決定事項」「次にやること」を書き換える
- 過去の状態を残したい場合は書き換えず `archive/` に日付付きでコピーしてから更新する
- このファイルは常に現在時点の状態のみを反映する（変更履歴は `docs/roadmap.md` 側に置く）
