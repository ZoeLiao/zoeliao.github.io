# Resource Requirements

## Kube-Scheduler
- When you specify a Pod, you can optionally specify how much of each resource a Container needs. The most common resources to specify are CPU and memory (RAM); there are others.

- When you specify the resource request for Containers in a Pod, the scheduler uses this information to decide which node to place the Pod on. When you specify a resource limit for a Container, the kubelet enforces those limits so that the running container is not allowed to use more of that resource than the limit you set. The kubelet also reserves at least the request amount of that system resource specifically for that container to use.

- If resources are not enough, the status of pod will be pending.

## Resource Requests
- Container:
    - default:
        - CPU: 0.5 == 500m 
        - Memory: 256 Mi
        - Disk
    - Note:
        - CPU:
            - Minimum: 0.1
            - 1 CPU ==:
                - 1 AWS vCPU
                - 1 GCP Core
                - 1 Azure Core
                - 1 Hyperthread
        - Memory:
            - 1 G (Gigabyte) == 10 ^ 9 bytes
            - 1 M (Megabyte) == 10 ^ 6 bytes
            - 1 K (Kilobyte) == 10 ^ 3 bytes
            - 1 Gi (Gigibyte) == 2 ^ 30 bytes
            - 1 Mi (Megibyte) == 2 ^ 20 bytes
            - 1 Ki (Kilibyte) == 2 ^ 10 bytes
- pod.yaml
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: webapp
      labels:
        name: webapp
    spec:
      containers:
      - name: webapp
        image: webapp
        ports:
          containerPort: 8080
        resources:
          requests:
            memory: "2Gi"
            cpu: 1
          limits:
            memory: "3Gi" <- can > throttle, but the pod will be terminated
            cpu: 2        <- can not > throttle
    ```
   
   
   
   
## Reference
- [Offical Doc - Managing Resources for Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)
   
