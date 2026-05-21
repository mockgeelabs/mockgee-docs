# Rate Limits and Quotas

Mockgee SaaS applies rate limits and quotas at the platform level to protect the management API and mock dataplane.

Rate limits are not configured per endpoint from the workspace UI. They are resolved from workspace entitlements and platform defaults.

## Runtime Dataplane Limits

Mock runtime requests are checked against workspace entitlements. When a workspace exceeds its allowed request volume or rate, Mockgee returns a `429` response.

The effective limits depend on the workspace plan:

- Free workspaces have lower request and running mock limits.
- Pro and Enterprise workspaces are intended for higher volume and team usage.
- Enterprise limits can be adjusted by the platform operator.

## Management API Protection

The management API also has abuse protection for signed-in SaaS operations, with stricter throttling around authentication routes.

This protects:

- sign in and sign up flows
- password reset attempts
- workspace administration APIs
- mock creation and update APIs

## What Happens When A Limit Is Reached

When a request is blocked by quota or rate limiting, the client receives a `429 Too Many Requests` response.

Typical next steps:

1. Check **Administration -> Billing** for current plan and usage.
2. Reduce high-volume test loops if running locally or in CI.
3. Move to a higher plan or contact support for Enterprise limits.

## Usage Visibility

Dashboard metrics show invocation activity for the workspace, including total mock API calls, latency, status families, method breakdown, unmatched requests, and AI streaming usage.

## Related Pages

- [Billing and Plans](billing.md)
- [Dashboard and Metrics](monitoring.md)
- [API Keys](api-keys.md)
