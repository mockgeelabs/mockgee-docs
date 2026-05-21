# MCP Server Simulation

Mockgee can expose selected tool mocks through an MCP-compatible server endpoint. This lets agent clients and developer tools test MCP integrations against deterministic responses.

## Create an MCP Server

1. Open **Build -> AI Mocks**.
2. Select **MCP Server**.
3. Create a server profile.
4. Set a name and slug.
5. Select the tools this server should expose.
6. Save.

## Runtime Endpoint

```text
POST /mockgee/mcp/server/:slug
```

Example:

```bash
export MCP_URL="https://<workspace>.<MOCK_BASE_DOMAIN>/mockgee/mcp/server/customer-support"
```

## Initialize

```bash
curl "${MCP_URL}" \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "initialize",
    "params": {
      "protocolVersion": "2024-11-05",
      "capabilities": {},
      "clientInfo": {
        "name": "demo-client",
        "version": "1.0.0"
      }
    }
  }'
```

## List Tools

```bash
curl "${MCP_URL}" \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "tools/list"
  }'
```

## Call a Tool

```bash
curl "${MCP_URL}" \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 3,
    "method": "tools/call",
    "params": {
      "name": "customer.lookup",
      "arguments": {
        "customerId": "cus_123"
      }
    }
  }'
```

## Current Scope

Mockgee supports the core streamable HTTP JSON-RPC subset:

- `initialize`
- `ping`
- `tools/list`
- `tools/call`
- empty resources and prompts catalogs

Resources, prompts, bearer-token MCP auth profiles, and replay/assertion governance are planned follow-up capabilities.
