# Troubleshooting

## Mock Request Returns Workspace Not Found

Check that you are calling the mock dataplane domain:

```text
https://<workspace>.<MOCK_BASE_DOMAIN>
```

For local development, use:

```text
http://<workspace>.localhost:8085
```

If using a custom domain, confirm it is verified under **Administration -> Domains**.

## Duplicate Endpoint Error

Create the endpoint under the correct project type: REST API, GraphQL API, or AI API. AI chat mocks are managed under **Build -> AI Mocks** and use `/v1/chat/completions`.

## Streaming Does Not Appear Token by Token

Confirm the client uses streaming mode and does not buffer output:

```bash
curl -N "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/chat/completions" ...
```

If a reverse proxy sits in front of Mockgee, disable response buffering for the mock dataplane.

## Tool Call Fails Validation

Check the tool input schema under **Build -> AI Mocks -> Tool Calls**. The request body must pass the schema before Mockgee evaluates rules.

## MCP Server Lists No Tools

Open **Build -> AI Mocks -> MCP Server** and confirm:

- the server is active
- at least one active tool is selected
- the tool itself has rules
- the client is calling `/mockgee/mcp/server/:slug`

## Account Deletion Is Blocked

Remove other active workspace members under **Administration -> Users** before deleting the account.

## No Dashboard Traffic

Make sure the app is calling the mock dataplane URL, not the management UI URL. Dashboard usage appears after runtime requests hit the mock dataplane.
