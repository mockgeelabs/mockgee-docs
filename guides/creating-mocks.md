# Creating Mocks

Mockgee organizes REST and GraphQL mock behavior under API Mocks. AI chat, Tool Calls, and MCP simulation live under AI Mocks.

## Creation Options

| Option | Use it when |
| --- | --- |
| Manual endpoint | You need one precise REST or GraphQL behavior. |
| Template | You want a realistic starter API quickly. |
| Import | You already have OpenAPI, Postman, or a Mockgee native export. |
| AI Chat mock | Your app calls OpenAI-compatible chat completions. |
| Tool Call | Your agent calls deterministic business tools. |
| MCP Server | Your MCP client needs mock tools exposed through MCP. |

## REST Endpoint

1. Open **Build -> API Mocks**.
2. Select **New endpoint**.
3. Choose **REST API**.
4. Configure:
   - project name
   - HTTP method
   - path
   - response status
   - response headers
   - response body
5. Save the endpoint.

Runtime example:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/orders/123"
```

## GraphQL Operation

1. Open **Build -> API Mocks**.
2. Select **New endpoint**.
3. Choose **GraphQL API**.
4. Configure the GraphQL path, operation type, operation name, and response.
5. Save the endpoint.

Mockgee matches GraphQL requests by explicit `operationName` or by deriving the operation name from the query string.

## AI Chat Mock

1. Open **Build -> AI Mocks**.
2. Select **Chat Completions**.
3. Create a chat mock.
4. Configure model, prompt matcher, assistant response, token metadata, and streaming behavior.
5. Save and call `/v1/chat/completions` on the mock dataplane.

## Advanced Behavior

After the basic endpoint works, add behavior as needed:

- request matchers for path, query, header, or body-specific responses
- fake data placeholders such as `$$.uuid`, `$$.timestamp`, and `$$.enum(...)`
- latency simulation
- fault/error injection
- default responses
- response mapping
- webhook dispatch on match

## Validate Before Sharing

Use the inline endpoint tester or the endpoint cURL sample to verify the response before sharing the mock URL with an app or test suite.
