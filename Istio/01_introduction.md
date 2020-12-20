# Introduction

## Service Mesh
- an extra layer of software you deploy alongside your cluster, e.g., K8s.
- K8s is not good at managing, giviing any visibility at the interconnect between the pods.
- A Service Mesh is a layer of software that is sitting underneath all of the pods.
- All calls will be directed via Service Mesh, e.g., A container <-> Service Mesh <-> B container, so that Service Mesh can provide:
    - Telemetry (遙測): gather metrics of individaul network requests, e.g., response time, response status.
    - Tracing: allow developers to take arbitrarily complex chains of network calls.
    - Security.
    - Traffic management: re-routing.

## Istio
- Istio is a Service Mesh. It injects into pods with a "Proxy" container to hanlde the interconnect between pods. This pattern is called "sidecar".
    - container A <-> proxy A <-> proxy B <-> container B 
- Jargon term:
    - Data Plane:
        - the collective term of the proxies that istio put into microservices.
    - Control Plane:
        - Istio-telemetry (pod)
        - Istio-pilot (pod)
        - Istio-tracing (pod)
- ![istio_architecture_1.8.svg](https://istio.io/latest/docs/ops/deployment/architecture/arch.svg)

- It can:
    - Connect, secure, control and observe services
    - Give you a graphical view to the pod level.
    - Distributed tracing: know how a single request works.
    - Allow you to alter traffic flow without modifying any application code.
