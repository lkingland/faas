# TypeScript CloudEvent Function

Welcome to your new TypeScript function project! The boilerplate function code can
be found in [`index.ts`](./index.ts). This function is meant to respond
exclusively to [Cloud Events](https://cloudevents.io/), but you can remove the
check for this in the function and it will respond just fine to plain vanilla
incoming HTTP requests.

## Local execution

To run locally

```console
npm install
npm run build
npm run local
```

The runtime will expose three endpoints.

  * `/` The endpoint for your function.
  * `/health/readiness` The endpoint for a readiness health check
  * `/health/liveness` The endpoint for a liveness health check

The health checks can be accessed in your browser at
[http://localhost:8080/health/readiness]() and
[http://localhost:8080/health/liveness](). You can use `curl` to `POST` an event
to the function endpoint:

```console
curl -X POST -d '{"name": "Tiger", "customerId": "0123456789"}' \
  -H'Content-type: application/json' \
  -H'Ce-id: 1' \
  -H'Ce-source: cloud-event-example' \
  -H'Ce-type: dev.knative.example' \
  -H'Ce-specversion: 1.0' \
  http://localhost:8080
```

The readiness and liveness endpoints use
[overload-protection](https://www.npmjs.com/package/overload-protection) and
will respond with `HTTP 503 Service Unavailable` with a `Client-Retry` header if
your function is determined to be overloaded, based on the memory usage and
event loop delay.

## Testing

This function project includes a [unit test](./test/unit.ts) and an
[integration test](./test/integration.ts).  Modify these, or add additional tests for your business logic.

```console
npm test
```
