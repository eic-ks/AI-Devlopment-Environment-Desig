# Request 006: 統合アーキテクチャ提案

- ステータス: 未着手
- 対応するCLAUDE.md節: 6. アーキテクチャ提案
- 依存: Phase 1〜5の結論（暫定結論でも可）
- 成果物置き場: `outputs/architecture/`

## 目的

Phase 1〜5で個別に検討したSkills・Workflow・Context/RAG・Knowledge Management・指示方法を、技術要素を含めた1つのアーキテクチャとして統合する。

## 出発点として与えられている技術要素（CLAUDE.mdより）

- MCP
- RAG
- Knowledge Graph
- Workflow Engine
- Agent / Subagent
- Memory
- ベクトルDB

技術選定も歓迎されているが、Phase 0の前提（個人利用・抽象設計）に照らして、過剰な基盤導入を提案していないか`docs/principles.md`の「導入コスト」軸で必ず検証する。

## 検討すべき問い

- 上記の技術要素それぞれについて、「今のスケール（個人利用）で本当に要るか／将来要るか／要らないか」を仕分けする
- Knowledge Graphのような重い仕組みは、Phase 4のKnowledge Management設計の代替になり得るか、補完か
- Subagent（このClaude Code環境で実際に使えるAgent機能）を、Phase 2のWorkflowの実行主体としてどう位置づけるか
- 各要素をどう組み合わせても、Phase 3で決めたAGENT.md/RAGの境界線と矛盾しないか

## 成果物

1. 統合アーキテクチャ図（要素間のデータフロー・呼び出し関係）
2. 各技術要素の採否とその理由（導入する/しない/将来検討）
3. Phase 1〜5の結論との整合性チェック

## このフェーズ開始時に確認すべきこと

Phase 1〜5がどこまで完了しているか確認し、未完了部分は暫定結論として扱う旨をこの成果物に明記する。
