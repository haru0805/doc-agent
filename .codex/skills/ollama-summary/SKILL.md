---
name: Ollama要約
description: ローカルOllamaを使って記事を要約する
---

## API仕様
POST http://localhost:11434/api/generate

---

## デフォルトモデル
phi3

---

## リクエスト形式
{
  "model": "phi3",
  "prompt": "次の記事を日本語で要約してください:\n{{TEXT}}",
  "stream": false
}

---

## 出力
Ollamaのレスポンス内の
"response"フィールドを使用する
