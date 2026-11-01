# Useful External Skills (Engineering)

ソフトウェアエンジニアリング・開発ワークフローで有用な外部スキルの一覧です。

## 一覧

| スキル | 取得元 | 概要 |
| --- | --- | --- |
| `karpathy-guidelines` | [`multica-ai/andrej-karpathy-skills`](https://github.com/multica-ai/andrej-karpathy-skills) | Andrej Karpathy の原則に基づく、LLM コーディングの典型的な失敗（過剰な抽象化・不要な変更・勝手な推測）を防ぐガイドライン |
| `grill-me` | [`mattpocock/skills`](https://github.com/mattpocock/skills) | 計画や設計の曖昧な点を徹底的に質問・深掘りして要件を固めるスキル |
| `grill-with-docs` | [`mattpocock/skills`](https://github.com/mattpocock/skills) | ドキュメントやコードベースを踏まえて設計・仕様をレビュー・深掘りするスキル |
| `find-skills` | [`vercel-labs/skills`](https://github.com/vercel-labs/skills) | 新しい機能やワークフローに対応する Agent Skills を検索・発見するスキル |
| `brainstorming` | [`obra/superpowers`](https://github.com/obra/superpowers) | 実装に入る前に要件・設計の選択肢・トレードオフを対話的に整理するブレインストーミングスキル |

## 導入コマンド (`npx skills`)

```bash
# グローバル (~/.claude/skills, ~/.agents/skills 等) に導入する場合 (-g)
npx skills@latest add multica-ai/andrej-karpathy-skills --skill karpathy-guidelines -g
npx skills@latest add mattpocock/skills --skill grill-me --skill grill-with-docs -g
npx skills@latest add vercel-labs/skills --skill find-skills -g
npx skills@latest add obra/superpowers --skill brainstorming -g
```

特定のプロジェクトのみに導入する場合は `-g` を外して実行してください。
