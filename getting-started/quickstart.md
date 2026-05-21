# Quick Start

This guide gets you from signup to a working mock endpoint.

## 1. Sign Up

1. Open your Mockgee SaaS URL.
2. Sign up with email or Google.
3. Mockgee creates your first workspace automatically.
4. Complete or skip onboarding.

Workspace administration lives under **Administration**. You do not need to create a tenant manually.

## 2. Understand the URLs

Mockgee separates management traffic from mock runtime traffic.

| Purpose | URL pattern |
| --- | --- |
| Management UI | `https://<workspace>.<APP_BASE_DOMAIN>` |
| Mock dataplane | `https://<workspace>.<MOCK_BASE_DOMAIN>` |

For local development:

| Purpose | URL |
| --- | --- |
| Management control plane | `http://<workspace>.localhost:8001` |
| Mock dataplane | `http://<workspace>.localhost:8085` |

## 3. Create Your First REST Endpoint

1. Go to **Build -> API Mocks**.
2. Select **New endpoint**.
3. Choose **REST API**.
4. Enter a project name, method, path, response status, headers, and body.
5. Save the endpoint.

Example endpoint:

```text
GET /v1/customers/123
```

Example response:

```json
{
  "id": "cus_123",
  "name": "Acme Inc",
  "plan": "pro"
}
```

## 4. Call the Mock

Production:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/customers/123"
```

Local development:

```bash
curl "http://<workspace>.localhost:8085/v1/customers/123"
```

## 5. Explore Core Workflows

- **API Mocks**: REST and GraphQL mock APIs.
- **AI Mocks**: OpenAI-compatible chat completions, Tool Calls, and MCP server simulation.
- **Inline testing**: verify mock responses from each endpoint or use the generated cURL sample.
- **Dashboard**: view invocation stats, latency, unmatched requests, and method breakdowns.
- **Administration**: users, billing, domains, audit, API keys, and settings.

## 6. Invite Your Team

Open **Administration -> Users** to invite teammates. Account deletion is blocked while another active workspace member remains.
