# Request Matcher

Request matching decides which saved sample Mockgee returns for an incoming request.

Mockgee first matches by HTTP method and path. It can then use request details such as path parameters, query values, headers, and request body to choose the right sample.

## What Can Be Matched

| Request part | Use for |
| --- | --- |
| Method | Separate `GET`, `POST`, `PUT`, `PATCH`, and `DELETE` behavior |
| Path | Match static paths such as `/v1/customers` |
| Path parameters | Match paths such as `/v1/customers/{id}` or `/v1/customers/:id` |
| Query parameters | Differentiate requests such as `?status=active` |
| Headers | Match API version, authorization shape, request IDs, or client type |
| Body | Match JSON/XML request payloads for non-GET methods |

## Path Parameters

Create a mock path with a parameter:

```text
GET /v1/customers/{id}
```

Then use a sample path value such as:

```json
{
  "id": "cus_123"
}
```

At runtime, a request to `/v1/customers/cus_123` can match that sample.

You can also echo the path value in a response:

```json
{
  "id": "{{request.path.id}}",
  "name": "{{faker.person.fullName}}"
}
```

## Query Matching

Use query parameters when the same endpoint returns different responses by filter.

Example:

```text
GET /v1/orders?status=pending
GET /v1/orders?status=shipped
```

Create separate samples with different query values to return different bodies.

## Header Matching

Use header matching for versioning, client behavior, auth simulation, or correlation IDs.

Example headers:

```json
{
  "x-api-version": "2026-05",
  "x-client-type": "mobile"
}
```

Response templates can also echo incoming headers:

```json
{
  "requestId": "{{request.headers.x-request-id}}"
}
```

## Body Matching

For `POST`, `PUT`, and `PATCH` mocks, request body matching lets you return different samples for different payloads.

Example:

```json
{
  "paymentMethod": "card",
  "amount": 1000
}
```

Create another sample for a different payload to simulate validation errors, edge cases, or alternate business outcomes.

## Multiple Matching Samples

If more than one sample matches the same request, endpoint rules can choose which sample is served:

- **First match:** serve the first matching sample
- **Random:** choose a matching sample at random
- **Weighted:** bias selection by per-sample weight
- **Sequence:** rotate across matching samples

Configure this from **Endpoint rules -> Scenario selection**.

## No Matching Sample

If no sample matches, endpoint rules decide the fallback:

- return `404`
- serve a default response
- proxy to an upstream API

Configure this from **Endpoint rules -> Fallback mode**.

## Related Pages

- [Dynamic Mocking](dynamic-mock.md)
- [Fake Data and Templates](fake-data.md)
- [Default Responses](../guides/default-responses.md)
