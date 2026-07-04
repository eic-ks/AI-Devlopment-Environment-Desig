# 引継ぎメモ（Handoff）

CLAUDE.mdの課題2「新しいチャットへ移る際、前チャットの内容を要約して引き継ぐと、情報が欠けたり表現が変わったりして意図しない方向へ進む」への対策。

**方針：自然文で要約しない。構造化された定型フォーマットで機械的に埋める。** 要約者（自分）の解釈が入る余地を減らすことが目的。

## 使い方

1. フェーズ（または長くなったセッション）を終える時、下の「最新の引継ぎ」ブロックを**今回の内容で上書き**する
2. 上書き前の内容は `archive/handoff/` に日付付きファイルとしてコピーしてから上書きする（履歴を残す）
3. 新しいチャットの最初にこのファイルの「最新の引継ぎ」だけを読めば再開できる状態を保つ

## テンプレート

```
### 完了したフェーズ
- Phase X: <フェーズ名>

### 確定した決定事項（変更しない前提）
- <決定1>（根拠：<理由>、記録先：<ファイルパス>）
- <決定2>

### 保留・要確認事項（次セッションで先に聞くこと）
- <question 1>

### 次セッションが最初に読むべきファイル
- <path1>
- <path2>

### 次にやる具体アクション
1. <action>
2. <action>
```

---

## 最新の引継ぎ

### 完了したフェーズ
- Phase 1: Skills設計（旧引継ぎは `archive/handoff/2026-07-02-phase0.md`）
- Phase 1追補: 全19Skillの実装（Claude Code形式SKILL.md、`skills/` 配下＋`~/.claude/skills/` へsymlink済み）

### 確定した決定事項（変更しない前提）
- Skillの粒度は「1成果物1Skill」。分割判定は「手順が違えば分割、基準・対象が違うだけならパラメータ化」（根拠：粒度判定を感覚でなく基準で行うため、記録先：`docs/decisions/0001-skill-granularity.md`）
- 階層は「カテゴリ→Skill」の2層分類階層のみ。実行階層は禁止、実行合成はWorkflowの責務（記録先：同ADR）
- プロジェクト固有知識はSkillに埋め込まず前提入力として注入する「注入原則」（記録先：`outputs/skills/02-design-principles.md` 原則1）
- Skill体系は6カテゴリ19Skill：理解系A(4)/計画系B(3)/変換系C(4)/評価系D(2)/記録系E(3)/セッション管理系F(3)（記録先：`outputs/skills/01-skill-catalog.md`）
- 「実装」そのものはSkillにしない。Workflow内の作業ステップとし、B系（前）とD系（後）で品質を挟み込む（記録先：`outputs/skills/01-skill-catalog.md` §2.1）
- 引継ぎは専用Skill（F1 context-handover）として独立。F系のみ厳格テンプレート・自由要約禁止（記録先：同 §2.2・§8）
- ADR-0003「設計ドキュメントのみ」を部分改定し、Phase 1のSkillsに限りClaude Code形式で実装した。設計（`outputs/skills/`）が正、実装（`skills/`）は変換層。変更は設計→実装の一方向（根拠・詳細：`docs/decisions/0006-build-executable-skills.md`）

### 保留・要確認事項（次セッションで先に聞くこと）
- 「前提入力の注入が欠けたまま実行された場合に進めずに要求する」規約はSkill定義単体では担保できない。Phase 2（Workflow）またはPhase 3（Context）で「入力欠落時の停止規約」を設計すること（ADR-0001の「結果・トレードオフ」参照）

### 次セッションが最初に読むべきファイル
- `docs/current-state.md`
- `requests/002-workflows.md`
- `outputs/skills/01-skill-catalog.md`（Phase 2の入力。特に§1の一覧と§2の整理）
- `outputs/skills/02-design-principles.md`（特に「Skill/Workflow/Contextの責務境界」節）

### 次にやる具体アクション
1. `requests/002-workflows.md` の「検討すべき問い」5つを確認し、Workflow設計を開始する
2. Phase 1で確定したSkill一覧（19Skill）を入力として、シナリオ別Workflow（新機能追加／バグ修正／リファクタリング／調査のみ等）を設計する
3. 上記保留事項「入力欠落時の停止規約」をWorkflow設計に組み込むか検討する
4. 成果物ができ次第 `outputs/workflows/` に保存し、`docs/current-state.md` と本ファイルを更新する
