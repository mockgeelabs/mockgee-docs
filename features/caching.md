# Runtime Caching

Mockgee SaaS uses Redis-backed runtime caching internally to keep mock lookup and workspace resolution fast. This is platform behavior, not a per-endpoint feature users configure from the UI.

## What Is Cached

Mockgee caches runtime data that is safe to rebuild from PostgreSQL:

- workspace and custom-domain resolution
- enabled mock lookup data
- endpoint rule configuration
- mock config records such as fallback behavior

PostgreSQL remains the durable source of truth. Redis cache failures should not change the saved mock configuration.

## When Cache Is Refreshed

Mockgee invalidates or refreshes runtime cache after important configuration changes, including:

- mock create, update, delete, enable, or disable
- endpoint rule changes
- workspace subdomain updates
- custom domain add, verify, or remove

## What Users Need To Know

Most users do not need to configure caching directly.

If a recently changed mock does not behave as expected:

1. Confirm the mock was saved successfully.
2. Confirm the request is hitting the mock dataplane, not the management UI.
3. Retry the request after a short delay.
4. Check Dashboard unmatched requests to confirm whether the request matched the expected endpoint.

## Not A Response Cache

Mockgee currently does not expose a user-facing response cache editor for individual mocks. Dynamic templates, Faker values, request-aware templates, and scenario selection are evaluated at request time.

## Related Pages

- [Dashboard and Metrics](monitoring.md)
- [Custom Domains](custom-domains.md)
- [Default Responses](../guides/default-responses.md)
