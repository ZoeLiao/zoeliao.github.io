# 3. Telemetry

## Requirements
- 1. Need a Proxy (Envoy Sidecar) running in each pod you want to monitor.
- 2. The control plane needs to be running (ie istiod, kiali, jaeger, and grafana).
- 3. You do not need any specific Istio yaml configuration. 
(No need for VirtualServices, Gateway, etc)

## Kiali
- Service mesh management for Istio
- It visualizes the traffic:
    - Graph:
        - app graph
        - workload graph
            - traffic
            - logs
            - inbound metrics
            - outbound metrics
        - service graph
- It allow you to:
    - make dynamic changes
    - circuit breaker
    - A / B test
    - You don't need to have staging env
- When you click "action" to:
    - Create Weighted Routing
    - Create Matching Routing 
    - Suspend Traffic
- Kiali will generate yamls to create the following resources to achieve the goal dynamically:
    - virtualservices, `kubectl get virtualservices,`
    - destinationrules, `kubectl get destinationrules,`

## Jeager
- You can not view single request in Kiali, but you can view the details in Opentracing frameworks

- Open Tracing:
    - Jeager: released by Uber
    - Zipkin: released by Twitter
- Trace:
    - a visualization of the life of a request as it moves through a distributed system.
- Span:
    - is the primary building block of a distributed trace, representing an individual unit of work done in a distributed system.
    - Each span encapsulates the following state according to the OpenTracing specification:
        - An operation name
        - A start timestamp and finish timestamp
        - A set of key:value span Tags
        - A set of key:value span Logs
        - A SpanContext

## References
- [OpenTelemetry](https://opentelemetry.io/docs/concepts/data-sources/)
