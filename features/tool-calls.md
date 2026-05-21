# Tool Calls

Tool Calls simulate deterministic agent tool execution. Use them for business actions such as customer lookup, ticket creation, order status, or eligibility checks.

## Create a Tool

1. Open **Build -> AI Mocks**.
2. Select **Tool Calls**.
3. Create a new tool.
4. Add a name such as `customer.lookup`.
5. Define an input JSON schema.
6. Optionally define an output JSON schema.
7. Save.

## Add Rules

Rules decide what the tool returns.

1. Select a tool.
2. Create a rule.
3. Configure match JSON.
4. Configure response JSON.
5. Optionally configure failure JSON.
6. Save.

## Runtime Endpoint

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/mockgee/tools/customer.lookup" \
  -H "Content-Type: application/json" \
  -d '{
    "arguments": {
      "customerId": "cus_123"
    }
  }'
```

If arguments fail the input schema, Mockgee returns a structured validation error instead of executing a rule.

## Invocation History

Tool Calls records recent invocations for debugging:

- successful matches
- missed matches
- schema validation failures
- tool execution failures
