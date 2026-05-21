# Custom Domains

Custom domains let a workspace serve mock runtime traffic from a domain your team controls.

## Add a Domain

1. Open **Administration -> Domains**.
2. Add the domain you want to use for mock runtime traffic.
3. Create the required DNS record.
4. Wait for verification.
5. Use the verified domain in your client or tests.

## Verification

Mockgee provides a DNS token for domain verification. Add the requested TXT record with your DNS provider. After the record propagates, Mockgee verifies ownership and routes runtime requests for that domain to your workspace.

## Runtime Use

```bash
curl "https://mock-api.example.com/v1/customers/123"
```

## Notes

- Custom domain availability depends on plan entitlements.
- Keep DNS records in place while the domain is active.
- Remove unused domains from **Administration -> Domains**.
