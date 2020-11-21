# Container Logging and Monitor

## Container Logging
- Command line:
    - Single container: `kubectl logs -f <pod name>`
    - Multiple container: `kubectl logs -f <pod name> <container name>`

## Framework
- e.g., Metrics server, Prometheus, Elastic Stack, Datadog, dynatrace

### Metrics Server
- Heapster is deprecated and it became metrics server.
- Aggregrate data from containers and store in memory.
- To cAdvisor (container advisor): expose containers to kube API for the metrics server.
- How to use:
    - minikube: minikube addons enable metrics-server
    - git clone https://github.com/kubernetes-incubator/metrics-server
    - kubectl create -f deploy/1.8+/
    - check:
        - kubectl top node
        - kubectl top pod
