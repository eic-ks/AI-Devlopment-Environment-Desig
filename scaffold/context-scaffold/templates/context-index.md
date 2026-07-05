# context/INDEX.md — 知識マニフェスト

Skillの前提入力【必須】と、それを満たすファイルの対応表。この対応の唯一の置き場。
ステップ開始時、該当行のパスに「ファイルが存在し空でない」ことを確認してから開始する。
欠落していれば開始せず、ユーザーに要求して停止する（AGENT.md の停止規約）。

<!-- 運用注記:
- まだ使わないSkillの行は表に置かない。「行はあるがファイルが無い」は停止規約により停止を誘発する。使い始める時に、L3ファイルを作ってから行を追加する
- 各ファイルの更新日はファイル自身の先頭メタデータが正。この表に更新日の写しを持たせない
-->

| 前提入力【必須】 | 利用Skill | パス |
|---|---|---|
| ナレッジベースの構成と記録フォーマット | E3 knowledge-capture | context/kb-format.md |
| セッション開始時に読むファイルの規約 | F3 session-restore | AGENT.md 冒頭（L1に常駐） |

<!-- 追加候補（使うSkillが決まったら、ファイルを作ってから行を表へ移す）:
| レビュー観点チェックリスト | D1 checklist-code-review | context/review-checklist.md |
| 命名規則・アーキテクチャ層の定義 | C1 refactor-rename / C3 refactor-restructure | context/naming-and-layers.md |
| テスト実行コマンド | C系共通・実装ステップ | context/test-commands.md |
| ドキュメントの文体・構成規約 | E1 documentation-update | context/doc-style.md |
| ADRテンプレートと採番規則 | E2 decision-recording | context/templates/adr.md |
| 引継ぎテンプレート | F1 context-handover | context/templates/handover.md |
| 状態ファイルのフォーマットと置き場 | F2 state-checkpoint | context/templates/state.md |
-->
