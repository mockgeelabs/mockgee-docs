# Best Practices

Use these practices to keep Mockgee workspaces easy to understand and reliable in test automation.

## Organize Mocks By API Boundary

Create one API Mock for each logical API or service boundary.

Good examples:

- `Customer API`
- `Payments API`
- `Orders API`
- `Public GraphQL API`

Avoid mixing unrelated domains in the same mock API. AI chat mocks, Tool Calls, and MCP simulation belong under **AI Mocks**.

## Prefer Clear Paths And Descriptions

Use realistic paths and short descriptions so teammates can quickly understand what a sample is for.

Examples:

- `GET /v1/customers/{id}` - customer found
- `POST /v1/payments` - card declined
- `GET /v1/orders` - pending orders

## Use Templates For Realistic Data

Use `{{...}}` templates for new dynamic responses.

Examples:

```json
{
  "id": "{{uuid}}",
  "name": "{{faker.person.fullName}}",
  "email": "{{faker.internet.email}}",
  "createdAt": "{{now 'iso'}}"
}
```

Use legacy `$$.` placeholders only when maintaining existing mocks.

## Keep Matching Specific

Start with the smallest matcher that proves the scenario.

Use:

- path parameters for resource-specific behavior
- query parameters for filtered lists
- headers for version/client behavior
- body matching for command-style requests

Avoid over-matching every header or body field unless the test needs that precision.

## Model Common Failure Paths

For each important API, add representative error samples:

- validation failure
- unauthorized request
- dependency unavailable
- rate limit response
- malformed or incomplete downstream response

Use fault injection for intermittent behavior and explicit samples for deterministic tests.

## Keep Fallback Behavior Intentional

Endpoint rules let unmatched requests return `404`, serve a default response, or proxy upstream.

Use:

- `404` while authoring strict mocks
- default response for broad client compatibility
- proxy fallback for hybrid integration tests

## Use Inline Testing Before Sharing URLs

After creating or changing an endpoint:

1. Open the API Mock detail page.
2. Use the inline test action.
3. Copy the cURL sample if the mock should be shared with another app or CI job.
4. Check Dashboard metrics after the first real runtime call.

## Separate Secrets From Mock Data

Do not put real passwords, customer identifiers, tokens, or production payloads in mock responses.

Use:

- placeholder values
- Faker data
- workspace API keys stored in a secret manager
- custom domains only after DNS verification

## Use AI Mocks For Agent Workflows

Use **AI Mocks** when testing:

- OpenAI-compatible chat completions
- streaming responses
- deterministic Tool Calls
- MCP server simulation

Keep AI behavior separate from REST and GraphQL API mocks so users understand where to configure each workflow.

## Review Usage Regularly

Use Dashboard metrics to check:

- total mock invocations
- status families
- method breakdown
- unmatched requests
- AI streaming activity
- latency trends

Unmatched requests are often the fastest way to discover a path, method, or matcher mismatch.
