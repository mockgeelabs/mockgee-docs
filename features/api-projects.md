# API Mocks

API Mocks are the main workspace area for REST and GraphQL mock APIs.

## Project Types

| Type | Use for |
| --- | --- |
| REST API | HTTP endpoints with methods, paths, status codes, headers, and bodies. |
| GraphQL API | GraphQL operation mocks on a GraphQL endpoint. |
| AI API | OpenAI-compatible chat completion mocks. AI-specific workflows are managed under **AI Mocks**. |

## Create a Mock

1. Open **Build -> API Mocks**.
2. Select **New endpoint** or start from a template/import.
3. Choose the API type.
4. Configure the endpoint or operation.
5. Save.

## Test a Mock

Every endpoint exposes a cURL sample. Use the mock dataplane domain:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/customers/123"
```

In local development:

```bash
curl "http://<workspace>.localhost:8085/v1/customers/123"
```

## Search

Use mock search to find APIs by name, type, or endpoint path.

## Recommended Workflow

1. Create or import the first mock API.
2. Test the endpoint with inline testing or cURL.
3. Add request matchers and default responses.
4. Watch dashboard invocation stats and unmatched request insights.
