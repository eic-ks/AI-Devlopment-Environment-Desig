# 現在地（Single Source of Truth）

**新しいチャットではまずこのファイルを読む。** CLAUDE.mdやこれまでの会話履歴を遡って再構築する必要はない。

## 今のフェーズ

**Phase 4（Knowledge Management設計）完了（2026-07-05） → Phase 5（AIへの指示方法）待ち**

## 確定済みの決定事項

| 決定 | 内容 | 記録場所 |
|---|---|---|
| 成果物形式 | 設計ドキュメント基本。使う道具はClaude Code形式で実装済み（`skills/`・`workflows/`・`scaffold/`）。判断基準・原則系は設計のまま | `docs/decisions/0003-deliverable-format.md`、`0006-build-executable-skills.md`、`0009-build-executable-workflows-and-scaffold.md` |
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
| KB内部構造（L4） | 分類は「知識の種類」5分類（知見・決定・外部情報・検索失敗・棚卸し）で固定・書き込みイベントと1対1・変更はADR必須。1エントリ1ファイル＋定型ヘッダ、命名 `{日付}-{短い説明}.md` でファイル名＝インデックス（インデックスファイル不保持）。重複排除・整合性は書き込み時glob+grep＋参照時矛盾検出の分散実行（全量チェックなし）。バージョン管理はGitのみ・失効マーキングか削除。Phase 3との矛盾ゼロを検証済み | `docs/decisions/0008-kb-structure.md`、`outputs/knowledge-management/00〜03` |
| Phase 2〜4の実行可能形式 | ADR-0003の部分改定②。W1〜W4＋組み立て規則を `workflows/` の5スキルに、Phase 3/4のContext/KB物理構造を `scaffold/context-scaffold`（雛形3種同梱・冪等）に実装。判断基準・原則系文書は設計のまま完了。設計が正・一方向ルールはADR-0006と同一。`~/.claude/skills/` へsymlink済み | `docs/decisions/0009-build-executable-workflows-and-scaffold.md`、`workflows/README.md`、`scaffold/README.md` |

## 未解決・要確認事項

- 適用作業3点は未実施：①このリポジトリのCLAUDE.md軽量化（`outputs/context-rag/02-placement-criteria.md` 5章で判定済み）②`context/kb-format.md` の実体化（内容＝`outputs/knowledge-management/01-kb-structure.md`）③`research/` の移行（同01の6章）。設計フェーズ完了後の適用作業として実施タイミングをユーザーに確認する
- 命名の質の劣化検出・死蔵エントリの誤情報・昇格の回数集計・降格の参照検出・棚卸し周期の計測 → Phase 7（運用設計）
- ~~Workflow・Context・KB体系の実行可能形式での実装は未決定~~ → 2026-07-05 に ADR-0009 で決定・実装済み（`workflows/`・`scaffold/`）

## 次にやること

1. `requests/005-instruction-methods.md` を読む
2. `outputs/skills/01-skill-catalog.md` と `outputs/workflows/01-workflow-catalog.md`・`02-orchestration-principles.md` を入力に、AIへの指示方法（タスク分割粒度・コンテキストの渡し方・レビュー依頼・Skills/Workflowを呼び出す指示の書き方）を設計し、`outputs/instruction-methods/` に成果物を保存する
3. 完了したらこのファイルと `docs/handoff.md` を更新する

## 更新ルール

- フェーズが1つ進むたびに「今のフェーズ」「確定済みの決定事項」「次にやること」を書き換える
- 過去の状態を残したい場合は書き換えず `archive/` に日付付きでコピーしてから更新する
- このファイルは常に現在時点の状態のみを反映する（変更履歴は `docs/roadmap.md` 側に置く）
