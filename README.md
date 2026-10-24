# my-skills

標準的な `skills/<name>/SKILL.md` レイアウトとネイティブプラグインマニフェストで管理される、個人のAIエージェント向けスキル集。自作スキルの管理・配布に加え、お気に入りの外部スキルを任意でプロジェクトへ同期できます。

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
package.json         外部スキルの選択・取得元と同期 CLI の定義
package-lock.json    同期 CLI の依存バージョン
skills-lock.json     同期した外部スキルの取得元・内容ハッシュ
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

### 4. お気に入りの外部スキルをまとめて同期する

Node.js 22.20.0 以上と npm、Git が必要です。リポジトリのルートで実行します。

```bash
# 新しい環境でも同じ手順
npm ci
npm run skills:sync
```

`package.json` の `skills` 配列に宣言した次の5スキルを、`skills experimental_sync` で同期します。

| 取得元 | スキル |
| --- | --- |
| `multica-ai/andrej-karpathy-skills` | `karpathy-guidelines` |
| `mattpocock/skills` | `grill-me`, `grill-with-docs` |
| `vercel-labs/skills` | `find-skills` |
| `obra/superpowers` | `brainstorming` |

**同期先はこのプロジェクト内のみです。** 実体を `.agents/skills/`（Codex 等の共有パス）に配置し、Claude Code 用のリンクを `.claude/skills/` に作成します。`~/.agents/skills/` や `~/.claude/skills/` へのグローバル導入は行いません。他のプロジェクトでも使う場合は、そのプロジェクトでの導入か、別途 `skills add -g` による導入が必要です。

自作の `skills/`、プラグイン定義、`scripts/link-skills.sh` はこの同期とは独立しています。外部スキルの実体は Git 管理せず、自作スキルにも同梱しません。`npm ci` だけではスキルを取得しないため、同期は明示的に実行してください。

#### 一覧の変更・更新

1. `package.json` の `skills` 配列で取得元 `source`、選択する `skills`、固定するコミット SHA `ref` を編集します。
2. `npm run skills:sync` を実行します。宣言から外した同期管理下のスキルは削除されます。
3. `package.json` と更新された `skills-lock.json` を一緒にコミットします。CLI の依存を変更した場合は `package-lock.json` も含めます。

再実行時は取得済みのスキルを再利用します。取得元の最新版を追従するには、`ref` を新しいコミット SHA に変更してから同期してください。`skills update` で別管理せず、この一覧を更新元にします。

同期は [実験的な CLI 機能](https://github.com/vercel-labs/skills/blob/main/docs/commands.md#experimental-commands) です。挙動の変更を避けるため CLI は `1.7.4`、外部スキルはコミット SHA で固定しています。`skills-lock.json` のみから復元する `experimental_install` ではエージェント固有のリンクが作られないため、このリポジトリでは新しい環境でも `npm run skills:sync` を使用します。

## スキル作成ワークフロー

1. `skills/<skill-name>/SKILL.md` にスキルを追加または更新する。
2. 詳細なチェックリストや資料は `skills/<skill-name>/references/` 以下に配置する。
3. 決定論的な再現性が重要な場合にのみ `skills/<skill-name>/scripts/` にスクリプトを追加する。
4. `docs/catalog.md` にスキルを記録する。
5. 新規スキルを追加した場合は `./scripts/link-skills.sh` を実行してローカルリンクを更新する。
