# Mockgee Documentation

Mockgee is a SaaS API simulation platform for REST, GraphQL, OpenAI-compatible AI mocks, deterministic Tool Calls, and MCP server testing.

## Start with the Product Flow

1. Sign up and use the workspace created for your account.
2. Create REST or GraphQL mocks under **Build -> API Mocks**.
3. Create AI chat mocks, Tool Calls, and MCP servers under **Build -> AI Mocks**.
4. Test runtime behavior from the mock dataplane URL.
5. Use dashboard metrics, inline mock testing, audit logs, API keys, domains, and billing from the workspace UI.

## Runtime URLs

| Surface | URL pattern |
| --- | --- |
| Management UI | `https://<workspace>.<APP_BASE_DOMAIN>` |
| Mock dataplane | `https://<workspace>.<MOCK_BASE_DOMAIN>` |

Local development commonly uses:

| Surface | URL |
| --- | --- |
| Management control plane | `http://<workspace>.localhost:8001` |
| Mock dataplane | `http://<workspace>.localhost:8085` |

## Core Documentation

- [Quick Start](getting-started/quickstart.md)
- [Creating Mocks](guides/creating-mocks.md)
- [API Mocks](features/api-projects.md)
- [AI Mocks](features/ai-mocks.md)
- [Tool Calls](features/tool-calls.md)
- [MCP Server Simulation](features/mcp-server.md)
- [Dashboard and Metrics](features/monitoring.md)
- [Troubleshooting](reference/troubleshooting.md)
