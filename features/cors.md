# CORS Support

Mockgee mock endpoints are designed to be callable from browser-based applications during development and testing.

## How CORS Works

The mock dataplane handles cross-origin requests and preflight traffic so frontend applications can call mock APIs from local or hosted environments.

Typical browser flows include:

- `OPTIONS` preflight requests
- `Content-Type` and `Authorization` request headers
- workspace subdomain mock URLs
- custom domain mock URLs

## Local Development

For local development, call the mock dataplane URL:

```text
http://<workspace>.localhost:8085
```

Do not call the management control plane for mock traffic:

```text
http://<workspace>.localhost:8001
```

## Production

Production mock traffic should use the mock base domain or a verified custom domain:

```text
https://<workspace>.<MOCK_BASE_DOMAIN>
https://api.your-domain.example
```

## Troubleshooting Browser Calls

If a browser request fails:

1. Confirm the URL points to the mock dataplane.
2. Confirm the endpoint path and HTTP method match a saved mock.
3. Check whether the browser is sending an `OPTIONS` preflight request.
4. Check Dashboard unmatched requests for the method and path.
5. If using a custom domain, confirm it is verified under **Administration -> Domains**.

## Related Pages

- [Custom Domains](custom-domains.md)
- [API Mocks](api-projects.md)
- [Troubleshooting](../reference/troubleshooting.md)
