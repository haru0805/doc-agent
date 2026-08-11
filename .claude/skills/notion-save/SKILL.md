---
name: notion-save
description: 要約結果を Notion データベースに保存する。Notion への書き込みノードやプロパティ設定を実装するときに使う。
---

# Notion 保存

## データベース構造
| プロパティ | 型 |
|---|---|
| タイトル | title |
| 日付 | date |
| 要約 | rich_text |
| URL | url |

## ルール
- 全フィールドを必ず設定する
- 日付は ISO 8601 形式
- 空フィールドを作らない
