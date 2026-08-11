---
name: n8n-workflow
description: 自動化タスク用のインポート可能な完全な n8n workflow JSON を生成する。n8n のワークフローやノード構成を作成・編集するときに使う。
---

# n8n ワークフロー生成

## 目的
インポート可能な n8n workflow JSON を生成する。

## ルール
- 必ずトリガーノードを含める
- ノード名は分かりやすくする
- 全ノードを接続する
- JSON を要求されたら JSON のみ出力する
- 最終出力にプレースホルダを残さない（環境変数・認証情報 ID を活用）

## 基本構成
```
Cron → データ取得 → 加工 → LLM → 保存
```

## Cron 設定
- 実行時間: 06:00
- タイムゾーン: Asia/Tokyo

## 参考
実装例: `workflow/workflow_note_pm_ollama_notion.json`
