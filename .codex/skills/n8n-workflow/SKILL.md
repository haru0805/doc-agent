---
name: n8nワークフロー生成
description: 自動化タスク用の完全なn8n workflow JSONを生成する
---

## 目的
インポート可能なn8n workflow JSONを生成する。

---

## ルール
- 必ずトリガーノードを含める
- ノード名は分かりやすくする
- 全ノードを接続する
- JSON要求時はJSONのみ出力

---

## 基本構成
Cron → データ取得 → 加工 → LLM → 保存

---

## Cron設定
- 実行時間：06:00
- タイムゾーン：Asia/Tokyo
