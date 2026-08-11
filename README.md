# doc-agent

n8n とローカル LLM（Ollama）を使って記事を自動要約し、Notion に保存するパイプライン。

## 概要

毎日 06:00（JST）に起動し、次の流れで動作する：

```
Cron (06:00 JST) → note RSS 46件を取得 → 前日更新を抽出 → Gemma で要約 → Notion に保存
```

- **クラウド API より ローカル処理を優先**（有料サービスは原則不使用）
- 自動化の中核は **n8n**、要約は **ローカル LLM（Gemma / Ollama）**

## ワークフロー

| ファイル | 内容 |
|---|---|
| `workflow/workflow_note_daily_gemma_notion.json` | note 著者フィード46件の前日更新記事を Gemma で要約して Notion に保存 |

取得対象の note フィード（46件）はワークフロー内の `Build Feed List` ノードに定義。追加・削除はここを編集する。

### 使い方
1. n8n に上記 JSON をインポートする
2. `YOUR_NOTION_DATABASE_ID` / `YOUR_NOTION_CREDENTIAL_ID` を自分の環境に合わせて設定
3. Ollama をローカルで起動（`http://localhost:11434`）し、`ollama pull gemma4:26b` でモデルを取得
4. Notion DB に `URL`(url) / `UpdatedDate`(date) / `Summary`(rich_text) プロパティを用意
5. ワークフローを有効化

## 技術スタック
Ubuntu / Docker / n8n（セルフホスト）/ Ollama / Notion API

## リポジトリ構成

```
doc-agent/
├── CLAUDE.md              # Claude Code 用のプロジェクト指示
├── README.md
├── workflow/              # n8n workflow JSON
├── .claude/skills/        # Claude Code 用スキル
├── .codex/                # Codex 用の指示・スキル
└── .github/               # GitHub Copilot 用の指示
```

各 AI エージェント向けの指示は上記の各ディレクトリに配置している。内容を変更する際は他の設定との同期も検討すること。
