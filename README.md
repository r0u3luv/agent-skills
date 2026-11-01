# my-skills

`skills/<category>/<name>/SKILL.md` レイアウトで管理される、個人のAIエージェント向けスキル集。

## ディレクトリ構成

```text
skills/              標準的な再利用可能スキル (skills/<category>/<name>/SKILL.md)
docs/                カテゴリ別の有用な外部スキル一覧
  engineering/       Engineering カテゴリの有用な外部スキル一覧
  finance/           Finance カテゴリの有用な外部スキル一覧
```

## インストールと使い方

### 1. スキルを導入する (`npx skills`)

Claude Code, Codex, Cursor など任意のハーネスへの導入や、特定のスキルのみの選択、ローカルクローンからのシンボリックリンク導入には `skills` CLI を使用します。

```bash
# GitHub から全スキルをグローバルにインストール
npx skills@latest add r0u3luv/skills -g

# 特定のスキルだけをインストール
npx skills@latest add r0u3luv/skills --skill code-review
npx skills@latest add r0u3luv/skills --skill pr-triage

# ローカルにクローンしたリポジトリからグローバルへリンク
npx skills@latest add . -g
```

### 2. 有用な外部スキルを導入する

外部の有用なスキルは本リポジトリには同梱せず、`docs/` 配下に `skills/` と同じカテゴリ階層（例: [`docs/engineering/external-skills.md`](docs/engineering/external-skills.md)）で整理しています。必要なスキルは `npx skills` で直接導入できます。

## スキル作成ワークフロー

1. `skills/<category>/<skill-name>/SKILL.md` にスキルを追加または更新する。
2. 詳細なチェックリストや資料は `skills/<category>/<skill-name>/references/` 以下に配置する。
3. 決定論的な再現性が重要な場合にのみ `skills/<category>/<skill-name>/scripts/` にスクリプトを追加する。
