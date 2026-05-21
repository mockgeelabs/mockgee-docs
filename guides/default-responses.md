# Default Responses

A default response is returned when an incoming request reaches a known endpoint but does not match a more specific request matcher.

## Configure a Default Response

1. Open **Build -> API Mocks**.
2. Select the project and endpoint.
3. Open the endpoint configuration.
4. Configure the fallback response body, status code, and headers.
5. Save the endpoint.

## Example

For `GET /v1/customers/{customerId}`, you might configure specific responses for known IDs and a default `404` for every other customer.

```json
{
  "error": {
    "code": "customer_not_found",
    "message": "No mock customer matched this request."
  }
}
```

## When to Use Default Responses

- Return clear errors for unknown IDs.
- Keep demos stable when a request does not match a known sample.
- Avoid random behavior during CI tests.
- Provide a baseline response while building more specific scenarios.
