# Introduction
- [Github - istio](https://github.com/istio/istio)
- [Website - istio](https://istio.io/)

## Service Mesh
- A service mesh is a way to increase the observability, resilience and security in a large-scale containerized application.
- Since K8s is not good at managing, giving any visibility at the interconnect between the pods.
- A Service Mesh is a extra layer of software that is sitting underneath all of the pods.
- All calls will be directed via Service Mesh, e.g., A container <-> Service Mesh <-> B container, so that Service Mesh can provide:
    - Telemetry (遙測): gather metrics of individaul network requests, e.g., response time, response status.
    - Tracing: allow developers to take arbitrarily complex chains of network calls.
    - Security.
    - Traffic management: re-routing.

## Istio
- Istio is a Service Mesh. It injects into pods with a "Proxy" container (Envoy)to hanlde the interconnect between pods with few or no code changes in service code. This pattern is called "sidecar".
    - container A <-> proxy A <-> proxy B <-> container B 
- Jargon term:
    - Data Plane:
        - the collective term of the proxies that istio put into microservices.
        - these proxies mediate and control all network communication between microservices.
        - they also collect and report telemetry on all mesh traffic.
    - Control Plane (Istiod):
        - manages and configures the proxies to route traffic.
            - Pilot: Responsible for configuring the proxies at runtime.
            - Citadel: Responsible for certificate issurance and rotation.
            - Galley: Responsible for validating, ingesting, aggregating, transforming and distributing config within Istio.
![istio_architecture_1.8.svg](https://istio.io/latest/docs/ops/deployment/architecture/arch.svg)

- Core features:
    - Traffic management:
        - easy rules configuration 
        - traffic routing
        - allow you to set up the following tasks easily:
            - A/B testing
            - canary rollouts
            - staged rollouts with percentage-based traffic splits.
        - out-of-box failure recovery features
    - Security: 
        - it provides:
            - the underlying secure communication channel
            - authentication
            - authorization
            - encryption of service communication at scale. 
        - it can secure pod-to-pod or service-to-service communication at the network and application layers.
    - Observability:
        - features:
            - tracing
            - monitoring
            - logging
        - custom dashboard
        - let you more effectively set, monitor, and enforce SLOs on services.

## Envoy
- Istio uses an extended version of the Envoy proxy. 
- Envoy is a high-performance proxy developed in C++ to mediate all inbound and outbound traffic for all services in the service mesh.
- Envoy proxies are the only Istio components that interact with data plane traffic.

## References
- [primer the who what and why of service mesh](https://thenewstack.io/primer-the-who-what-and-why-of-service-mesh)
- [Istio](https://istio.io/latest/)
- [Envoy](https://www.envoyproxy.io/)
