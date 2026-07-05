# workflows/ — 実行可能Workflow（Claude Code Skill形式）

`outputs/workflows/01-workflow-catalog.md`（設計）をClaude CodeのSKILL.md形式に変換した実装層。設計原則は `outputs/workflows/02-orchestration-principles.md` を参照。

## 運用ルール

- **設計（`outputs/workflows/`）が正、ここは実装**。変更は必ず設計→実装の一方向で行う。実装側で得た改善案は設計ドキュメント・ADRに昇格させてから反映する
- 利用は `~/.claude/skills/` への symlink 経由（全プロジェクト共通で使える）：
  ```bash
  cd workflows && for d in */; do ln -sfn "$PWD/${d%/}" ~/.claude/skills/"${d%/}"; done
  ```
- symlink 後の新しいセッションから `/workflow名` で呼び出せる（descriptionによる自動起動もあり）
- WorkflowはSkillを参照するため、`skills/` 側のsymlinkも設定済みであること（原則W6: WorkflowはSkillを知るが、SkillはWorkflowを知らない）

## カタログIDとディレクトリ名の対応

| ID | ディレクトリ名 | 内容 |
|---|---|---|
| W1 | `workflow-w1-feature` | 新機能追加 |
| W2 | `workflow-w2-bugfix` | バグ修正 |
| W3 | `workflow-w3-refactor` | リファクタリング |
| W4 | `workflow-w4-investigation` | 調査のみ |
| —（8〜9章） | `workflow-assembly` | テンプレート外シナリオの組み立て規則 |

Workflow内のSkill参照は `skills/README.md` の対応表に従う（C4=`code-cleanup`、D1=`checklist-code-review` に改名済み）。

## 共通外枠（セッションラッパー）

どのWorkflowにも、本体とは独立に常に適用される外枠がある（カタログ2章）。全Workflow共通のため、ここに一度だけ書く。

| タイミング | 使用Skill | 内容 |
|---|---|---|
| セッション再開時（Workflowの途中から始める時） | F3 session-restore | 状態ファイル・引継ぎドキュメントからコンテキストを復元し、再開計画メモを出してから本体に入る |
| 各ゲート到達時・作業中断時 | F2 state-checkpoint | どこまで進み、次の一手が何かを状態ファイルに保存する |
| フェーズ完了時・セッション終了時 | F1 context-handover | 定型テンプレートを充填した引継ぎドキュメントで閉じる |

**ゲート＝チェックポイント**（各ゲートでF2必須。原則W4）。セッションを切るならゲートで切り、「1セッション1ゲート区間」を推奨上限とする。再開は必ずF3経由で行う。

## 設計からの意図的な差分（変換時の判断）

- **Skill参照をID＋実装名の併記に変換**: カタログはSkillをIDのみで参照するが（原則W6）、実装層では呼び出し可能な名前が必要なため「D1 checklist-code-review」の形式で表記した。対応は `skills/README.md` の表に従う
- **共通規約の各SKILL.mdへの要約転記**: カタログ2章（共通外枠）・原則W3（入力欠落時の停止）・原則W4（ゲート＝チェックポイント）は設計上「毎回書かない」共通事項だが、各Workflowが単体のスキルとして起動された時に規約が落ちないよう、各SKILL.mdに「共通規約」節として3行で要約転記した。全体像は本READMEのみに置く
- **8章と9章を1スキルに統合**: 組み立て規則（8章）とテンプレート追加基準（9章）は「テンプレート外のシナリオに直面した時」に同時に参照されるため、`workflow-assembly` 1本にまとめた
- **章番号参照の読み替え**: カタログ内の「8章の組み立て規則に従い」等の参照は、実装層では `workflow-assembly` への参照に読み替えた
