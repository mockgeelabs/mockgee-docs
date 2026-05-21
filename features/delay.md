# Response Delay and Faults

Mockgee can simulate slow, unstable, or failing dependencies from each mock endpoint.

Use delay and fault settings to test loading states, timeout handling, retries, and degraded downstream behavior.

## Where To Configure It

1. Open **Build -> API Mocks**.
2. Create or edit a REST endpoint.
3. Open the resilience/timing section in the endpoint form.
4. Configure base delay, latency jitter, error rate, or connection drop behavior.
5. Save the endpoint.

## Delay

Base delay adds a fixed wait before Mockgee sends the response.

Example use cases:

- verify frontend loading states
- test client request timeout settings
- simulate slow partner APIs
- make CI tests exercise retry behavior

## Latency Jitter

Latency jitter adds a random extra delay on top of the base delay.

Use jitter when you want a response time range instead of the same delay on every call.

Example:

| Setting | Behavior |
| --- | --- |
| Base delay: `1s` | Every response waits at least 1 second |
| Jitter min: `200ms` | Adds at least 200ms more |
| Jitter max: `1200ms` | Adds up to 1200ms more |

## Error Injection

Error injection replaces a percentage of otherwise matched responses with a configured error response.

You can configure:

- error rate
- error status code
- error body

Use this for testing intermittent dependency failure without changing the happy-path mock.

## Connection Drop

Connection drop closes the request without returning the normal response.

Use it carefully: it is useful for timeout and network-error handling tests, but it can make automated tests intentionally flaky if enabled broadly.

## Best Practices

- Keep default mocks fast unless a test needs latency.
- Use small error rates for resilience tests.
- Create separate samples for deterministic error responses when you need predictable assertions.
- Document intentionally slow or failing mocks in the endpoint description.

## Related Pages

- [Dynamic Mocking](dynamic-mock.md)
- [Default Responses](../guides/default-responses.md)
- [Dashboard and Metrics](monitoring.md)
