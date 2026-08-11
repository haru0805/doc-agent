---
name: ollama-summary
description: ローカルの Ollama を使って記事本文を日本語で要約する。要約処理や Ollama API 呼び出しを実装するときに使う。
---

# Ollama 要約

## API 仕様
`POST http://localhost:11434/api/generate`

## デフォルトモデル
`gemma4:26b`

## リクエスト形式
```json
{
  "model": "gemma4:26b",
  "prompt": "以下の記事を、要点を落とさず日本語で3〜5個の箇条書きに丁寧に要約してください:\n{{TEXT}}",
  "stream": false,
  "options": { "temperature": 0.3 }
}
```

## 出力
Ollama のレスポンス内の `response` フィールドを使用する。
