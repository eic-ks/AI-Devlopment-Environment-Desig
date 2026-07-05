# scaffold/ — Context/KB構造の生成Skill（Claude Code形式）

`outputs/context-rag/`（Phase 3: 5層配置モデル）と `outputs/knowledge-management/`（Phase 4: KB内部構造）の設計を、対象プロジェクトにContext/KB物理構造一式を生成するSkill `context-scaffold` として実装した層。

## 運用ルール

- **設計（`outputs/context-rag/`・`outputs/knowledge-management/`）が正、ここは実装**。変更は必ず設計→実装の一方向で行う。実装側で得た改善案は設計ドキュメント・ADRに昇格させてから反映する
- 利用は `~/.claude/skills/` への symlink 経由（全プロジェクト共通で使える）：
  ```bash
  cd scaffold && ln -sfn "$PWD/context-scaffold" ~/.claude/skills/context-scaffold
  ```
- symlink 後の新しいセッションから `/context-scaffold` で呼び出せる（descriptionによる自動起動もあり）

## テンプレートと設計ドキュメントの対応

| テンプレート | 生成先 | 由来する設計 |
|---|---|---|
| `context-scaffold/templates/agent-md.md` | 常駐ファイル（AGENT.md/CLAUDE.md、L1） | `outputs/context-rag/01-context-architecture.md` 2章（L1の置くもの・置かないもの）・4.1（停止規約の常駐）、`02-placement-criteria.md` 1章（3テスト）・2章（150行予算） |
| `context-scaffold/templates/context-index.md` | `context/INDEX.md`（L3） | `outputs/context-rag/01-context-architecture.md` 4.2（知識マニフェスト・対応表の形式と例）・4.3（存在判定と停止の挙動） |
| `context-scaffold/templates/kb-format.md` | `context/kb-format.md`（L3。E3 knowledge-capture の【必須】入力の実体） | `outputs/knowledge-management/01-kb-structure.md` 1〜3章の構造化転記（5分類表・構造・命名規則・定型ヘッダ・分類別テンプレート） |
| （テンプレートなし。Skillが直接作成） | `knowledge/` 5分類ディレクトリ（L4） | `outputs/knowledge-management/01-kb-structure.md` 1章（5分類）・2章（2段構造） |

## 設計からの意図的な差分（変換時の判断）

1. **常駐ファイルの既定名を `CLAUDE.md` とした**: 設計は常駐ファイルを汎用名 AGENT.md で規定し物理名は自由とする（`01-context-architecture.md` 冒頭の用語規定）。本SkillはClaude Code形式の実装であるため、生成時の既定名を Claude Code が自動読み込みする `CLAUDE.md` にした（任意入力で `AGENT.md` 等に変更可）。テンプレート中の `AGENT.md` 表記は生成時に実名へ機械置換する
2. **INDEX雛形の行の絞り込み**: 設計（`01-context-architecture.md` 4.2）の対応表例は9行だが、雛形の表には生成時点で実体が揃う2行（`context/kb-format.md`・F3の「AGENT.md 冒頭」）のみを置き、残り7行はコメント内の「追加候補」とした。理由: 「行はあるがファイルが無い」状態は停止規約（4.3）により停止を誘発するため、未作成ファイルを指す行を初期状態に含めない
3. **決定（ADR）の置き場の既定**: 設計は「既存のADR置き場をそのまま充ててよい」とする（`01-kb-structure.md` 1章）。Skillは既定で `knowledge/decisions/` を生成し、既存のADR置き場を検出した場合は報告して選択を人間に委ねる（Skillに置き場の設計判断をさせない）
4. **雛形内のプレースホルダコメント**: `agent-md.md` の各節にあるHTMLコメント（ここに何を書くか／書いてはいけないか）は設計にない記入ガイドであり、記入後に削除する運用を雛形とSKILL.mdに注記した
5. **空ディレクトリの `.gitkeep`**: Gitが空ディレクトリを追跡しないための実装上の措置（設計には現れない）
