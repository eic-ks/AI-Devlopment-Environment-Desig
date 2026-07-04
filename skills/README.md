# skills/ — 実行可能Skill（Claude Code形式）

`outputs/skills/01-skill-catalog.md`（設計）をClaude CodeのSKILL.md形式に変換した実装層。経緯と決定は `docs/decisions/0006-build-executable-skills.md` を参照。

## 運用ルール

- **設計（`outputs/skills/`）が正、ここは実装**。変更は必ず設計→実装の一方向で行う。実装側で得た改善案は設計ドキュメント・ADRに昇格させてから反映する
- 利用は `~/.claude/skills/` への symlink 経由（全プロジェクト共通で使える）：
  ```bash
  cd skills && for d in */; do ln -sfn "$PWD/${d%/}" ~/.claude/skills/"${d%/}"; done
  ```
- symlink 後の新しいセッションから `/skill名` で呼び出せる（descriptionによる自動起動もあり）

## カタログIDとディレクトリ名の対応

設計上のIDと実装名は原則同一。組み込みスキルとの衝突回避のため2つのみ改名した。

| ID | ディレクトリ名 | 備考 |
|---|---|---|
| A1 | `codebase-mapping` | |
| A2 | `flow-tracing` | |
| A3 | `dependency-analysis` | |
| A4 | `impact-analysis` | |
| B1 | `requirement-clarification` | |
| B2 | `implementation-planning` | |
| B3 | `test-planning` | |
| C1 | `refactor-rename` | |
| C2 | `refactor-extract` | |
| C3 | `refactor-restructure` | |
| C4 | `code-cleanup` | 設計名 cleanup から改名 |
| D1 | `checklist-code-review` | 設計名 code-review から改名（組み込み /code-review と衝突） |
| D2 | `artifact-self-review` | |
| E1 | `documentation-update` | |
| E2 | `decision-recording` | |
| E3 | `knowledge-capture` | |
| F1 | `context-handover` | フォールバックテンプレート同梱 |
| F2 | `state-checkpoint` | フォールバックテンプレート同梱 |
| F3 | `session-restore` | |

## 設計からの意図的な差分（変換時の判断）

- **停止規約の実装**: 「前提入力の欠落時に進めずに要求する」を各SKILL.mdの前提入力欄に明記（ADR-0001で持ち越した規約への部分回答。Workflow/Context側の設計はPhase 2/3で行う）
- **F1/F2のフォールバックテンプレート**: プロジェクト規約が無い場合のみ使う汎用テンプレートを同梱。プロジェクト固有知識ではないため注入原則には反しない
- **D1はデフォルト観点を持たない**: 設計上の明示的決定を維持。チェックリスト未注入なら停止する
