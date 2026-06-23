# my-skills

APMファースト（Agent Package Managerファースト）のレイアウトで管理される、個人のAIエージェント向けスキル集。

## 戦略

`.apm/` を一次情報源（Source of Truth）として使用し、このリポジトリ自体を APM パッケージとして他のプロジェクトから参照します。外部で再利用したいスキルは `apm.yml` の依存関係に追加し、各プロジェクトではこのリポジトリを `apm install` します。

## ディレクトリ構成

```text
.apm/
  skills/          標準的な再利用可能スキル
  instructions/    共通の動作およびエンジニアリングの基本方針
  prompts/         再利用可能なプロンプトテンプレート
  agents/          役割別のエージェント定義
adapters/
  claude-plugin/   Claude Codeプラグイン用パッケージングのメモ
  codex/           Codex向け運用メモ
  copilot/         GitHub Copilot向け運用メモ
  cursor/          Cursor向け運用メモ
  windsurf/        Windsurf向け運用メモ
docs/              人間用カタログおよび作成ガイド
tests/             スキル検証用フィクスチャ
```

## 他のプロジェクトで使う

対象プロジェクトのルートで、このリポジトリを APM 依存としてインストールします。

```bash
cd /path/to/target-project
apm install /Users/ruo/Project/my-tools/rou0-skills --target codex
```

これにより、対象プロジェクト側の `apm.yml` にこのリポジトリが依存関係として追加され、`apm.lock.yaml` に解決結果が固定されます。このリポジトリの `.apm/` と `apm.yml` に記述した外部依存関係も、APM の依存解決対象になります。

対象プロジェクトに `.codex/` や `.cursor/` などのハーネスマーカーがない場合、APM は展開先を自動判定できません。継続的に同じ対象へ展開するプロジェクトでは、対象プロジェクトの `apm.yml` に `targets:` を明示します。

```yaml
targets:
  - codex
```

## グローバルにスキルをインストールする

ユーザー全体で使えるようにする場合は、`-g` または `--global` を指定します。

```bash
apm install --global /Users/ruo/Project/my-tools/rou0-skills
```

特定のスキルだけをインストールする場合は、`--skill` を併用します。

```bash
apm install --global /Users/ruo/Project/my-tools/rou0-skills --skill pr-triage
```

このリポジトリ内で実行する場合も、グローバルインストールでは絶対パスを指定します。

```bash
apm install --global /Users/ruo/Project/my-tools/rou0-skills --skill pr-triage
```

複数のスキルを指定する場合は、`--skill` を繰り返します。

```bash
apm install -g /Users/ruo/Project/my-tools/rou0-skills --skill pr-triage --skill code-review
```

対象ランタイムを絞る場合は、`--target` を併用します。

```bash
apm install -g /Users/ruo/Project/my-tools/rou0-skills --target codex --skill code-review
```

全スキルに戻す場合は、`--skill '*'` を指定します。

```bash
apm install -g /Users/ruo/Project/my-tools/rou0-skills --skill '*'
```

## 依存関係の管理とインストール (Dependencies & Installation)

APM (Agent Package Manager) を使用して、外部リポジトリ（GitHubなど）で公開されているスキルをこのリポジトリの依存関係として管理します。

このリポジトリの `apm.yml` の `dependencies` セクションに外部スキルを記述します。

```yaml
dependencies:
  apm:
    - multica-ai/andrej-karpathy-skills
    - git: mattpocock/skills
      skills:
        - grill-me
```

設定後、このリポジトリ内で以下を実行すると依存関係を解決し、バージョンを固定するための `apm.lock.yaml` を生成します。

```bash
apm install
```

配布用にスナップショット化したい場合は bundle を作成できます。

```bash
apm pack --archive
```

## 運用ルール

- まず `.apm/` を編集すること。
- 外部で使えそうなスキルは `apm.yml` の依存関係として追加すること。
- 各 `SKILL.md` は簡潔に保ち、詳細な資料は `references/` に移動すること。
- 決定論的な再現性が重要な場合にのみスクリプトを追加すること。
- 共有する前に、現実的なフィクスチャを使用して重要なスキルを検証すること。

## 初期ワークフロー

1. `.apm/skills/<skill-name>/SKILL.md` にスキルを追加または更新する。
2. `.apm/skills/<skill-name>/references/` 以下に関連するリファレンスを追加する。
3. `docs/catalog.md` にスキルを記録する。
4. 必要に応じて `apm install` で lockfile を更新する。
