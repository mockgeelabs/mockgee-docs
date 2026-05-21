# Dynamic Mocking

Dynamic mocking lets one endpoint return different behavior based on the incoming request and endpoint rules.

Use it when a static response is not enough: different users, statuses, request payloads, failure cases, fallback behavior, or scenario rotation.

## Core Concepts

| Concept | Purpose |
| --- | --- |
| Samples | Multiple saved responses for the same method and path |
| Request matchers | Query, header, path, and body criteria that select a sample |
| Scenario selection | First, random, weighted, or sequence selection when multiple samples match |
| Fallback mode | What happens when no sample matches |
| Templates | Runtime data generation and request-aware response values |

## Multiple Samples

You can create more than one sample for the same endpoint.

Example:

```text
GET /v1/customers/{id}
```

Sample 1 can return a Pro customer:

```json
{
  "id": "{{request.path.id}}",
  "name": "{{faker.person.fullName}}",
  "plan": "pro"
}
```

Sample 2 can return a suspended customer:

```json
{
  "id": "{{request.path.id}}",
  "name": "{{faker.person.fullName}}",
  "plan": "pro",
  "status": "suspended"
}
```

## Request-Specific Responses

Use matchers when the same endpoint should respond differently for different inputs.

Examples:

- `GET /v1/orders?status=pending`
- `GET /v1/orders?status=shipped`
- `POST /v1/payments` with `{ "paymentMethod": "card" }`
- `POST /v1/payments` with `{ "paymentMethod": "wallet" }`

## Scenario Selection

When two or more samples match the same request, endpoint rules decide which sample is served:

- **First match:** deterministic default behavior
- **Random:** uniform random choice
- **Weighted:** biased random choice based on per-sample weight
- **Sequence:** round-robin behavior across samples

Configure this from **Endpoint rules -> Scenario selection**.

## Fallback Behavior

When no sample matches, endpoint rules can:

- return `404`
- serve a default response
- proxy the request to an upstream API

Configure this from **Endpoint rules -> Fallback mode**.

## Dynamic Response Data

Use `{{...}}` templates for runtime values:

```json
{
  "transactionId": "{{uuid}}",
  "timestamp": "{{now 'iso'}}",
  "customerName": "{{faker.person.fullName}}",
  "amount": "{{random 10 5000}}",
  "status": "{{one-of 'pending' 'completed' 'failed'}}",
  "reference": "{{sequence 'transactions'}}"
}
```

Mockgee also supports legacy `$$.` placeholders for existing mocks. For new mocks, prefer `{{...}}` templates because they support Faker and request-aware values such as `{{request.path.id}}`, `{{request.query.limit}}`, and `{{request.body.email}}`.

## Error And Resilience Cases

Dynamic mocking works well with delay and fault settings.

Use explicit samples for deterministic outcomes:

```json
{
  "error": "Card declined",
  "code": "payment_declined"
}
```

Use fault injection when the client should experience intermittent failure.

## Recommended Workflow

1. Create the happy-path sample first.
2. Add request matchers only where behavior needs to differ.
3. Add error samples for deterministic test cases.
4. Use scenario selection for random, weighted, or sequence behavior.
5. Add fallback behavior only when unmatched requests should be handled deliberately.
6. Verify with inline testing and Dashboard unmatched requests.

## Related Pages

- [Request Matcher](request-matcher.md)
- [Fake Data and Templates](fake-data.md)
- [Default Responses](../guides/default-responses.md)
- [Delay and Faults](delay.md)
