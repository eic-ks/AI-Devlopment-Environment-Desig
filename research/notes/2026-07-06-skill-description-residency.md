# 気づき: Skill description の常駐コスト問題（Phase 7 検討対象）

- 記録日: 2026-07-06（Phase 6 完了後のプロジェクト棚卸し中に発見。ユーザー承認済み: Phase 7 の課題に含める）
- 分類: スコープ外の気づき → Phase 7（統合・長期運用）へ

## 事実

- `~/.claude/skills/` に25本（19 Skill＋5 Workflow＋context-scaffold）をsymlink運用中（ADR-0006・0009）
- Claude Code の機構では、インストール済みSkillの **frontmatter（name＋description）は使用有無に関係なく全セッションのシステムプロンプトに常駐**する。実測 約7.9KB ≒ 3,000〜4,000トークン／セッション。全プロジェクトに波及する
- SKILL.md 本文（40〜60行）がロードされるのは呼び出し時のみ。本文のトークン効率設計は機能している。問題は本文ではなく**メタデータの常駐**

## 設計上の緊張

- Phase 3 の5層モデルは L5定義層を「呼び出し時に読む」と位置づけたが、実機構では **L5のdescriptionはL1（常駐層）として振る舞う**。L1には3テスト＋150行予算の規律があるのに、description総量には相当する規律がない
- コストはSkill数に比例して増える。ADR-0001 の見直し閾値「Skill数30超」に、分類管理とは別にトークン観点からも圧力がかかる
- このプロジェクト自身では日常語彙（引継ぎ・ADR・自己レビュー・チェックポイント）がF系・E系Skillのdescriptionと一致しやすく、意図しない自動起動も起きやすい（設計どおりの動作ではある）

## Phase 7 で検討する選択肢（2026-07-06時点の素案）

- (a) description の分量規律を新設する（L1の分量予算と同型の「description予算」。例: 1本あたり1文＋トリガー語）
- (b) 配布単位の見直し: グローバル（`~/.claude/skills/`）→ プロジェクト単位（`.claude/skills/`）で使うものだけ載せる
- (c) 遅延ロード方式: 常駐は最小の索引だけにして、必要時に全文を引く（Claude Code の Tool Search / deferred tool loading と同型の解。Tool Use における「全ツール定義の常駐」問題と同じ問題クラス）
- いずれも「設計（outputs/）が正・一方向変換」ルールの対象。実施するなら ADR または Phase 7 成果物として決定してから実装へ反映する

## 関連

- ADR-0001（Skill数30超の見直し条件）・ADR-0006/0009（symlink配布）・`outputs/context-rag/01-context-architecture.md`（5層モデル・L1分量予算）
