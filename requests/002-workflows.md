# Request 002: Workflow設計

- ステータス: 未着手
- 対応するCLAUDE.md節: 2. Workflow設計
- 依存: Phase 1（Skills設計）
- 成果物置き場: `outputs/workflows/`

## 目的

Skillsをどう組み合わせるかを設計する。Skill単体ではなく、複数Skillのオーケストレーションのパターンを汎用化する。

## 前提

Phase 1で確定したSkills一覧（`outputs/skills/`）を入力として使う。Phase 1が未完了なら、暫定のSkills候補（`requests/001-skills.md`記載）を仮置きして進めてもよいが、その旨をADR/成果物に明記する。

## 出発点として与えられている例（CLAUDE.mdより）

新機能追加のWorkflow例：

```
Codebase Analysis → Implementation Planning → Implementation → Review → Refactor → Documentation Update → Context Update
```

このWorkflowを前提とせず、他のシナリオ（バグ修正、リファクタリングのみ、既存コード調査のみ等）でも通用する形に一般化してよい。

## 検討すべき問い

- Workflowは「固定順序のパイプライン」か「条件分岐のあるステートマシン」か
- どこでユーザー（自分）の承認・レビューを挟むべきか（全自動と全手動の間のどこに線を引くか）
- 同じSkillを複数のWorkflowが共有する時、Workflow定義はどこに置くべきか
- Workflowの長さ（フェーズ数）が長すぎて「長い会話で迷子になる」課題を再発させないためのWorkflow設計上の工夫は何か
- Workflow自体もSkill同様に汎用テンプレートとして持つべきか、それとも都度その場で組み立てるものか

## 成果物

1. Workflow一覧（シナリオ別：新機能追加／バグ修正／リファクタリング／調査のみ 等）
2. 各Workflowが使うSkillの組み合わせと順序
3. 分岐・承認ポイントの設計原則

## このフェーズ開始時に確認すべきこと

Phase 1の結果（確定したSkills一覧）を先に読み込むこと。
