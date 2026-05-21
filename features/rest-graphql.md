# REST and GraphQL

Mockgee supports REST endpoint mocks and GraphQL operation mocks in API Mocks.

## REST Mocks

REST mocks match normal HTTP requests by method and path.

1. Open **Build -> API Mocks**.
2. Select **New endpoint**.
3. Choose **REST API**.
4. Configure method, path, response code, headers, and response body.
5. Save and test from the mock dataplane.

Example:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/orders/ord_123"
```

## GraphQL Mocks

GraphQL mocks are configured as GraphQL operations. Mockgee matches incoming GraphQL requests by the JSON `operationName` field or by deriving the operation name from the query string.

1. Open **Build -> API Mocks**.
2. Select **New endpoint**.
3. Choose **GraphQL API**.
4. Configure the GraphQL path, operation name, operation type, and response.
5. Save and call the endpoint from your GraphQL client.

Example request:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/graphql" \
  -H "Content-Type: application/json" \
  -d '{
    "operationName": "GetCustomer",
    "query": "query GetCustomer { customer { id name } }"
  }'
```

## Avoiding Duplicate Paths

REST, GraphQL, and AI project types are separate product workflows. If two projects need the same method/path, create them under the appropriate type so each workflow remains clear.
