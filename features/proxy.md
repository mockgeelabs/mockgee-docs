# Proxy Fallback

Proxy fallback forwards unmatched requests for an endpoint to an upstream API.

Use it when you want a hybrid test setup: Mockgee serves the cases you have modeled, and an existing service handles anything that does not match a saved sample.

## Where To Configure It

1. Open **Build -> API Mocks**.
2. Open a mock API.
3. Select an endpoint.
4. Open **Endpoint rules**.
5. Under **Fallback mode**, choose **Proxy**.
6. Enter the upstream target URL and authentication settings.
7. Save configuration.

Proxy fallback only runs when no saved sample matches the incoming request.

## Supported Settings

| Setting | Description |
| --- | --- |
| Target URL | Upstream URL to forward unmatched requests to |
| Timeout | Maximum upstream wait time in seconds |
| Authentication | No Auth, Basic Auth, API Key, or Bearer Token |
| API key placement | Header or query parameter |

## Runtime Behavior

When proxy fallback is active:

1. Mockgee first tries to match a saved sample.
2. If a sample matches, Mockgee serves that sample.
3. If no sample matches, Mockgee forwards the incoming method and body to the configured upstream target.
4. Dashboard metrics record the request as proxied.

## Security Guardrails

Mockgee validates outbound proxy targets to reduce SSRF risk.

Blocked targets include private networks, cloud metadata endpoints, internal-only hostnames, and non-HTTP schemes.

## Common Uses

- Mock only the endpoints under active development.
- Keep unmodeled endpoints flowing to a staging API.
- Capture edge cases by adding samples over time while still allowing broader integration tests to run.

## Related Pages

- [Default Responses](../guides/default-responses.md)
- [Dynamic Mocking](dynamic-mock.md)
- [Dashboard and Metrics](monitoring.md)
