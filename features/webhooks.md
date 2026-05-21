# Webhooks

Webhooks let Mockgee notify another system when a mock endpoint is matched.

## Create a Webhook

1. Open **Build -> Webhooks**.
2. Create a new webhook.
3. Enter the destination URL.
4. Configure the signing secret and status.
5. Save.

## Attach a Webhook

1. Open **Build -> API Mocks**.
2. Select a mock API and endpoint.
3. Open **Endpoint rules**.
4. Configure the endpoint's webhook behavior.
5. Save.

When the endpoint matches at runtime, Mockgee dispatches the webhook asynchronously.

## Delivery Behavior

- Requests are signed with HMAC.
- Delivery retries use backoff.
- Webhook calls do not block the mock response path.

## Use Cases

- Notify a test harness that a mock was called.
- Trigger a downstream integration during a demo.
- Simulate event-driven behavior after an API request.
