# Fake Data and Response Templating

Mockgee supports two dynamic data systems:

- **Recommended:** `{{...}}` response templates for Faker data, request echoing, counters, timestamps, random values, and response/header templating.
- **Legacy:** `$$.` dynamic placeholders such as `$$.uuid`, `$$.timestamp`, and `$$.enum(...)`. Existing mocks continue to work.

Use the `{{...}}` template syntax for new mocks. It is more expressive because it can read the incoming request and use `@faker-js/faker` for realistic data.

## Where Templates Work

Templates are evaluated at runtime on matched mock responses.

They work in:

- JSON response body string values
- text response bodies
- XML response bodies
- response headers

Unknown `{{...}}` expressions are left unchanged, so literal template-looking text is safe.

## Faker Examples

Use `{{faker.<namespace>.<method>}}` to call Faker helpers.

```json
{
  "id": "{{uuid}}",
  "name": "{{faker.person.fullName}}",
  "email": "{{faker.internet.email}}",
  "company": "{{faker.company.name}}",
  "city": "{{faker.location.city}}",
  "createdAt": "{{now 'iso'}}"
}
```

Common examples:

| Template | Example output |
| --- | --- |
| `{{faker.person.fullName}}` | `Avery Johnson` |
| `{{faker.internet.email}}` | `avery.johnson@example.com` |
| `{{faker.location.city}}` | `Dubai` |
| `{{faker.company.name}}` | `Acme Solutions LLC` |
| `{{faker.phone.number}}` | `+1 555 123 4567` |
| `{{faker.number.int}}` | `48213` |
| `{{faker.string.uuid}}` | `b1f0c5e0-7b1d-4c3e-9f6c-9b3b8f0d7d52` |

Mockgee walks the Faker dotted path and calls the final method with no arguments. If a Faker helper needs required arguments, prefer one of Mockgee's built-in helpers below or use a static sample value.

## Built-In Template Helpers

| Helper | Description |
| --- | --- |
| `{{uuid}}` | Random UUID v4 |
| `{{now}}` | Current Unix epoch in milliseconds |
| `{{now 'iso'}}` | Current ISO-8601 timestamp |
| `{{now 'unix'}}` | Current Unix epoch in seconds |
| `{{random 1 100}}` | Random integer between 1 and 100 |
| `{{one-of 'pending' 'shipped' 'failed'}}` | Random value from the provided list |
| `{{sequence 'orders'}}` | Monotonic counter by workspace and sequence name |

Example:

```json
{
  "orderId": "ord_{{sequence 'orders'}}",
  "status": "{{one-of 'pending' 'paid' 'shipped'}}",
  "priority": "{{random 1 5}}",
  "issuedAt": "{{now 'iso'}}"
}
```

## Request-Aware Templates

Templates can copy values from the incoming request.

| Template | Reads from |
| --- | --- |
| `{{request.body.email}}` | Parsed JSON request body |
| `{{request.headers.x-request-id}}` | Request headers, looked up case-insensitively |
| `{{request.query.limit}}` | Query string |
| `{{request.path.id}}` | Path parameter from a mock path such as `/customers/{id}` or `/customers/:id` |

Example mock path:

```text
GET /v1/customers/{id}
```

Example response:

```json
{
  "id": "{{request.path.id}}",
  "requestId": "{{request.headers.x-request-id}}",
  "name": "{{faker.person.fullName}}",
  "email": "{{request.query.email}}",
  "servedAt": "{{now 'iso'}}"
}
```

Example call:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/customers/cus_123?email=test@example.com" \
  -H "x-request-id: req_001"
```

## Header Templates

Response headers can also use templates.

```json
{
  "x-mock-request-id": "{{request.headers.x-request-id}}",
  "x-mock-sequence": "{{sequence 'responses'}}"
}
```

## Legacy `$$.` Placeholders

Legacy dynamic placeholders remain supported for existing mocks.

| Placeholder | Description |
| --- | --- |
| `$$.uuid` | Unique identifier |
| `$$.ip` | IP address |
| `$$.name` | Random name |
| `$$.int(6)` | Integer with the requested length |
| `$$.ints(5)` | Numeric string with the requested length |
| `$$.float(4,2)` | Decimal number |
| `$$.timestamp` | Current ISO timestamp |
| `$$.boolean` | Random boolean |
| `$$.enum(red,green,blue)` | Random value from the list |

Example:

```json
{
  "id": "$$.uuid",
  "createdAt": "$$.timestamp",
  "status": "$$.enum(active,pending,inactive)"
}
```

For new mocks, prefer `{{...}}` templates because they support Faker and request-aware values.

## Choosing the Right Syntax

| Need | Use |
| --- | --- |
| Realistic names, emails, companies, addresses | `{{faker...}}` |
| Echo path, query, header, or body values | `{{request...}}` |
| Stable per-suite counters | `{{sequence 'name'}}` |
| Existing mocks already using `$$.` | Keep `$$.` |
| Simple random legacy values | `$$.` still works, but `{{...}}` is recommended |

## Notes and Limits

- Templates do not execute arbitrary JavaScript.
- There are no loops or conditionals in response templates.
- `{{sequence ...}}` counters are in-memory and reset when the server restarts.
- Faker helpers are called without custom arguments.
- Legacy `$$.` placeholders and `{{...}}` templates can coexist in the same response.

## Next Steps

- Learn about [Dynamic Mocking](dynamic-mock.md) for multiple responses and matchers.
- Review [Request Matcher](request-matcher.md) for request-specific responses.
- Use [Response Mapping](mapping.md) for request-to-response copy patterns.
