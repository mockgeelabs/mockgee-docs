# Response Mapping

Response mapping in the current SaaS version is handled through `{{...}}` response templates.

Use templates to copy request data into the mock response, generate realistic Faker data, add timestamps, or echo request headers.

## Request Mapping Syntax

| Template | Reads from |
| --- | --- |
| `{{request.body.email}}` | Parsed JSON request body |
| `{{request.headers.x-request-id}}` | Request headers |
| `{{request.query.limit}}` | Query string |
| `{{request.path.id}}` | Path parameters from `/customers/{id}` or `/customers/:id` |

## Example

Mock path:

```text
POST /v1/customers/{id}/orders
```

Response body:

```json
{
  "orderId": "ord_{{sequence 'orders'}}",
  "customerId": "{{request.path.id}}",
  "email": "{{request.body.email}}",
  "requestId": "{{request.headers.x-request-id}}",
  "status": "{{one-of 'pending' 'confirmed'}}",
  "createdAt": "{{now 'iso'}}"
}
```

Example request:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/customers/cus_123/orders" \
  -H "Content-Type: application/json" \
  -H "x-request-id: req_001" \
  -d '{"email":"customer@example.com"}'
```

Example response:

```json
{
  "orderId": "ord_1",
  "customerId": "cus_123",
  "email": "customer@example.com",
  "requestId": "req_001",
  "status": "confirmed",
  "createdAt": "2026-05-21T10:30:00.000Z"
}
```

## Header Mapping

Response headers can also use templates:

```json
{
  "x-request-id": "{{request.headers.x-request-id}}",
  "x-mock-sequence": "{{sequence 'responses'}}"
}
```

## Faker And Helpers

Templates can be mixed with Faker and built-in helpers:

```json
{
  "id": "{{uuid}}",
  "name": "{{faker.person.fullName}}",
  "company": "{{faker.company.name}}",
  "servedAt": "{{now 'iso'}}"
}
```

## Legacy Mapping

Older documentation referenced `$request...` mapping expressions and transformation functions. For the SaaS UI, use `{{request...}}` templates instead. Legacy dynamic `$$.` placeholders still work for existing mocks, but they do not read request data.

## Related Pages

- [Fake Data and Templates](fake-data.md)
- [Request Matcher](request-matcher.md)
- [Dynamic Mocking](dynamic-mock.md)
