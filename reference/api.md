# API Reference

This page summarizes the public runtime paths most users need. Management APIs are workspace-scoped and should be called from the management domain; mock runtime APIs are called from the mock dataplane domain.

## Runtime Base URL

```text
https://<workspace>.<MOCK_BASE_DOMAIN>
```

Local development:

```text
http://<workspace>.localhost:8085
```

## REST Mock

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/customers/123"
```

## GraphQL Mock

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/graphql" \
  -H "Content-Type: application/json" \
  -d '{
    "operationName": "GetCustomer",
    "query": "query GetCustomer { customer { id name } }"
  }'
```

## AI Chat Mock

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

## Streaming AI Chat Mock

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

## Tool Call

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/mockgee/tools/customer.lookup" \
  -H "Content-Type: application/json" \
  -d '{
    "arguments": {
      "customerId": "cus_123"
    }
  }'
```

## MCP Server

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/mockgee/mcp/server/customer-support" \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/list"
  }'
```

## API Keys

Workspace API keys use the `mgsk_` prefix.

```bash
curl "https://<MOCK_BASE_DOMAIN>/v1/customers/123" \
  -H "Authorization: Bearer mgsk_your_workspace_key"
```
