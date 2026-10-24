# my-skills

標準的な `skills/<name>/SKILL.md` レイアウトとネイティブプラグインマニフェストで管理される、個人のAIエージェント向けスキル集。

## ディレクトリ構成

```text
.claude-plugin/
  plugin.json        Claude Code / Codex / Copilot 用プラグイン定義
  marketplace.json   マーケットプレイス定義
skills/              標準的な再利用可能スキル (skills/<name>/SKILL.md)
agents/              役割別のサブエージェント定義
prompts/             再利用可能なプロンプトテンプレート
scripts/
  link-skills.sh     ローカル環境 (~/.claude/skills, ~/.agents/skills) へのシンボリックリンク作成
docs/                人間用カタログおよび作成ガイド
tests/               スキル検証用フィクスチャ
```

## インストールと使い方

### 1. ローカル開発・個人環境への即時反映（推奨）

このリポジトリをクローンしている環境では、`scripts/link-skills.sh` を実行すると `~/.claude/skills` と `~/.agents/skills` に各スキルのシンボリックリンクが作成されます。

```bash
./scripts/link-skills.sh
```

シンボリックリンクのため、`skills/<skill-name>/SKILL.md` を編集したり `git pull` するだけで、再インストール作業なしに Claude Code や Codex 等へ即時反映されます。

### 2. ネイティブプラグインとして導入する（自動更新）

各エージェントのプラグイン機構を使って GitHub リポジトリから直接購読できます。

**Claude Code:**

```bash
/plugin marketplace add r0u3luv/skills
/plugin install r0u3luv-skills@r0u3luv
```

**Codex:**

```bash
codex plugin marketplace add r0u3luv/skills
codex plugin add r0u3luv-skills@r0u3luv
```

**GitHub Copilot CLI:**

```bash
copilot plugin marketplace add r0u3luv/skills
copilot plugin install r0u3luv-skills@r0u3luv
```

**Gemini CLI:**

```bash
gemini skills install https://github.com/r0u3luv/skills.git --path skills
```

### 3. `npx skills` (skills.sh) で導入する（汎用・個別選択）

Cursor, Windsurf, OpenCode など任意のハーネスや、特定のプロジェクトへファイルとしてコピーしたい場合は `skills` CLI を使用します。

```bash
# 全スキルをインストール
npx skills@latest add r0u3luv/skills

# 特定のスキルだけをインストール
npx skills@latest add r0u3luv/skills --skill code-review
npx skills@latest add r0u3luv/skills --skill pr-triage
```

### 4. 外部スキルの導入について

外部で公開されているスキル（`mattpocock/skills`, `addyosmani/agent-skills`, `obra/superpowers` 等）は、このリポジトリに同梱・ラップせず、それぞれの公式プラグインまたは `npx skills` で直接導入します。

```bash
# 例: 外部スキルの個別導入
npx skills@latest add mattpocock/skills --skill grill-me --skill grill-with-docs
npx skills@latest add vercel-labs/skills --skill find-skills
npx skills@latest add obra/superpowers --skill brainstorming
```

## スキル作成ワークフロー

1. `skills/<skill-name>/SKILL.md` にスキルを追加または更新する。
2. 詳細なチェックリストや資料は `skills/<skill-name>/references/` 以下に配置する。
3. 決定論的な再現性が重要な場合にのみ `skills/<skill-name>/scripts/` にスクリプトを追加する。
4. `docs/catalog.md` にスキルを記録する。
5. 新規スキルを追加した場合は `./scripts/link-skills.sh` を実行してローカルリンクを更新する。
