# CLAUDE.md

このファイルは Claude Code がこのリポジトリで作業する際の指示です。

## プロジェクト概要
n8n とローカル LLM を使い、記事を自動要約して Notion に保存するパイプラインを構築する。

ワークフローの流れ：
1. 毎日 06:00（JST）に Cron 起動
2. note の RSS フィード（46件）から前日更新の記事を取得
3. ローカル LLM（Gemma / Ollama）で丁寧に要約
4. Notion データベースへ保存（1記事＝1行）

実装済みワークフロー: `workflow/workflow_note_daily_gemma_notion.json`
（note 著者フィード46件の前日更新記事を Gemma で要約して Notion に保存）
対象フィード一覧はワークフロー内 `Build Feed List` ノードに定義。

## 技術スタック
- Ubuntu / Docker
- n8n（セルフホスト）
- Ollama（ローカル LLM）
- Notion API

## 基本方針
1. クラウド API よりローカル処理を優先する
2. 有料サービスは使用しない（明示的な指示がある場合を除く）
3. 自動化の中核は n8n とする
4. ワークフローはシンプル・モジュール化・再利用可能にする
5. インポート可能な n8n workflow JSON を生成する

## Ollama API 仕様
- エンドポイント: `POST http://localhost:11434/api/generate`
- デフォルトモデル: `gemma4:26b`
- リクエスト: `{ "model": "gemma4:26b", "prompt": "...", "stream": false, "options": { "temperature": 0.3 } }`
- 出力: レスポンスの `response` フィールドを使用
- プロンプト方針: 記事本文全体を渡し、要点を落とさず日本語で3〜5個の箇条書きに丁寧に要約する

## Notion データベース構造
| プロパティ | 型 |
|---|---|
| タイトル | title |
| 日付 | date（ISO 8601） |
| 要約 | rich_text |
| URL | url |

## コーディングルール
- ワークフロー生成時は必ず有効な JSON を出力する
- JSON を要求されたら説明文を含めず JSON のみ出力する
- ノード名は分かりやすくする / 不要なノードは追加しない
- 全ノードを接続する
- 最終出力にプレースホルダを残さない（可能な限り環境変数を使う）

## スキル
`.claude/skills/` に作業別スキルを配置している：
- `n8n-workflow` — n8n workflow JSON の生成
- `ollama-summary` — Ollama での記事要約
- `notion-save` — 要約結果の Notion 保存

## 他エージェント向け設定
同じ内容を他ツール向けにも配置している（変更時は同期を検討）：
- Codex: `.codex/AGENT.md`, `.codex/skills/`
- GitHub Copilot: `.github/copilot-instructions.md`
