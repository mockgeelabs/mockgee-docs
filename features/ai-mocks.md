# AI Mocks

AI Mocks let teams test LLM-powered applications without calling a live model provider. The first supported runtime is OpenAI-compatible Chat Completions.

## Create an AI Chat Mock

1. Open **Build -> AI Mocks**.
2. Select **Chat Completions**.
3. Create a new chat mock.
4. Configure:
   - model
   - prompt matcher
   - assistant response
   - usage metadata
   - streaming behavior
5. Save.

## Runtime Endpoint

```text
POST /v1/chat/completions
```

Example:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-mini",
    "messages": [
      { "role": "user", "content": "Return the demo answer" }
    ],
    "stream": false
  }'
```

## Streaming

Enable streaming when testing token-by-token UI behavior.

```bash
curl -N "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-mini",
    "messages": [
      { "role": "user", "content": "Stream the demo answer" }
    ],
    "stream": true
  }'
```

Streaming mocks return `text/event-stream` chunks and terminate with:

```text
data: [DONE]
```

## Use Cases

- Test chat UI loading, streaming, and completion states.
- Run CI without model-provider cost or rate limits.
- Build deterministic demos.
- Reproduce edge cases that are hard to trigger with live providers.
