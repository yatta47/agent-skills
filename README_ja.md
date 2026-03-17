# agent-skills

[Claude Code](https://claude.ai/claude-code) と [Codex CLI](https://github.com/openai/codex) で使える汎用スキル・サブエージェント集。

[English](README.md) | 日本語

## スキル一覧

| スキル | 説明 |
|--------|------|
| [til-extract](skills/til-extract/) | 会話やファイルからTIL（Today I Learned）を抽出し、Markdownノートとして保存 |
| [session-feedback](skills/session-feedback/) | セッションを振り返り、プロジェクトルール・スキル・ワークフローの改善を提案 |
| [pretty-mermaid](skills/pretty-mermaid/) | Mermaid図をSVGやASCIIアートとして美麗にレンダリング（15種類以上のテーマ対応） |

## エージェント（サブエージェント）

| エージェント | 説明 |
|-------------|------|
| [codex-agent](agents/codex-agent.md) | Codex CLIをセカンドオピニオンとして活用。コードレビュー、設計相談、調査など |

## インストール

### Claude Code（skills.sh経由）

```bash
npx skills add yatta47/agent-skills
```

プロジェクトの `.claude/skills/` に直接インストールされます。

> **注意**: skills.sh ではスキルのみインストールされます。codex-agent サブエージェントを使うには手動でコピーしてください:
> ```bash
> mkdir -p .claude/agents
> curl -o .claude/agents/codex-agent.md https://raw.githubusercontent.com/yatta47/agent-skills/main/agents/codex-agent.md
> ```

### Claude Code（手動）

スキルとエージェントをプロジェクトにコピー:

```bash
git clone https://github.com/yatta47/agent-skills.git /tmp/agent-skills

# スキル
cp -r /tmp/agent-skills/skills/til-extract .claude/skills/
cp -r /tmp/agent-skills/skills/session-feedback .claude/skills/
cp -r /tmp/agent-skills/skills/pretty-mermaid .claude/skills/

# エージェント
mkdir -p .claude/agents
cp /tmp/agent-skills/agents/codex-agent.md .claude/agents/

rm -rf /tmp/agent-skills
```

### Codex CLI

クローンしてシンボリックリンク:

```bash
git clone https://github.com/yatta47/agent-skills.git vendor/agent-skills
ln -s vendor/agent-skills/skills .agents/skills
```

## 設定

### til-extract

デフォルトではプロジェクトルートの `til/` にTILファイルを保存します。保存先を変更するには `CLAUDE.md` に以下を追加:

```
TIL output directory: knowledge/til/
```

## クレジット

- `pretty-mermaid` は [intellectronica/agent-skills](https://github.com/intellectronica/agent-skills)（CC0-1.0）をベースにしています

## ライセンス

MIT
