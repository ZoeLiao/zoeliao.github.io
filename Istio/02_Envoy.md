# 2. Envoy

## Why not use Envoy directly?
- Service Mesh is one of application of Envoy.
- Envoy Proxy is capable of being deployed into many different types of cluster.
- It has a massive and complex terminology of its own.
- Istio simplifies envoy and allow us to use regular K8s yaml (via CRDs) to implement Envoy.

## Introduction
- [Website - Envoy](https://www.envoyproxy.io)
- Istio uses an extended version of the Envoy proxy. 
    - In Istio: Proxy = sidecar = Envoy
- Envoy is made by lyft.
- Envoy is a high-performance proxy developed in C++ to mediate all inbound and outbound traffic for all services in the service mesh.
- Envoy proxies are the only Istio components that interact with data plane traffic.
    - For example:
        - The metrics of tracing (Jeager, Kiali)
        - circut breaker
- Reverse Proxy in Envoy:
    - request -> Proxy -> target
    - The client knows they have called the proxy.
    - The client thinks the results have come from the proxy.

## References
- [Envoy](https://www.envoyproxy.io/)
