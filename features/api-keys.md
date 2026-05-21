# API Keys

API keys are workspace-scoped credentials for automation and integrations.

## Create an API Key

1. Open **Administration -> API Keys**.
2. Select **New API key**.
3. Give the key a recognizable name.
4. Copy the generated key immediately.
5. Store it in your secret manager or CI environment.

## Runtime Tenant Resolution

Mock runtime calls are normally routed by workspace subdomain:

```bash
curl "https://<workspace>.<MOCK_BASE_DOMAIN>/v1/customers"
```

When a workspace API key is supplied, Mockgee can also resolve the workspace from the key:

```bash
curl "https://<MOCK_BASE_DOMAIN>/v1/customers" \
  -H "Authorization: Bearer mgsk_your_workspace_key"
```

## Key Hygiene

- Store keys in a secret manager.
- Use separate keys per environment.
- Rotate keys when credentials change.
- Delete unused keys from **Administration -> API Keys**.
