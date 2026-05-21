# Mockgee SaaS Documentation

Mockgee helps teams build and test integrations without waiting on live systems. Create REST and GraphQL mock APIs, simulate OpenAI-compatible AI responses, test deterministic agent Tool Calls, and expose selected tools through MCP server endpoints.

## Start Fast

| Goal | Start here |
| --- | --- |
| Create your first mock API | [Quick Start](/getting-started/quickstart.md) |
| Build REST or GraphQL endpoints | [API Mocks](/features/api-projects.md) |
| Test OpenAI-compatible chat | [AI Mocks](/features/ai-mocks.md) |
| Mock agent tool execution | [Tool Calls](/features/tool-calls.md) |
| Connect an MCP client | [MCP Server Simulation](/features/mcp-server.md) |

## What You Can Simulate

### API Workflows

- REST endpoints with custom methods, paths, headers, status codes, and response bodies.
- GraphQL operation mocks matched by `operationName` or query text.
- Request-specific responses using path, query, header, and payload matchers.
- Fake data, response mapping, default responses, latency, and fault scenarios.

### AI and Agent Workflows

- OpenAI-compatible `POST /v1/chat/completions` responses.
- Streaming `text/event-stream` chat chunks ending with `data: [DONE]`.
- Deterministic Tool Calls with JSON schema validation and invocation history.
- MCP server profiles that expose selected active tools to MCP-compatible clients.

### Workspace Operations

- Import from OpenAPI, Postman, or Mockgee native exports.
- Verify mocks with inline endpoint testing, cURL samples, and dataplane calls.
- Watch invocation stats, latency, AI stream usage, and unmatched requests.
- Manage users, API keys, custom domains, billing, audit logs, and webhooks.

## Runtime Model

Mockgee separates management traffic from mock runtime traffic.

| Surface | Purpose | Example |
| --- | --- | --- |
| Management UI | Create mocks and manage workspace settings | `https://<workspace>.<APP_BASE_DOMAIN>` |
| Mock dataplane | Serve mock API, AI, Tool Call, and MCP traffic | `https://<workspace>.<MOCK_BASE_DOMAIN>` |

Local development commonly uses:

```text
http://<workspace>.localhost:8001      # management control plane
http://<workspace>.localhost:8085      # mock dataplane
```

## Common Runtime Examples

REST:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/customers/123"
```

AI chat:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -d '{"model":"gpt-4o-mini","messages":[{"role":"user","content":"Demo"}]}'
```

Tool Call:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/mockgee/tools/customer.lookup" \
  -H "Content-Type: application/json" \
  -d '{"arguments":{"customerId":"cus_123"}}'
```

MCP:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/mockgee/mcp/server/customer-support" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

## Recommended Reading

1. [Quick Start](/getting-started/quickstart.md)
2. [Creating Mocks](/guides/creating-mocks.md)
3. [Features Overview](/features/README.md)
4. [API Reference](/reference/api.md)
5. [Troubleshooting](/reference/troubleshooting.md)
