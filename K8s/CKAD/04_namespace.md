# Namespace

## Default
- Includes 
    - Resource Limits
        - ```yaml
          spec:
            hard:
              pods: "5"
              requests.cpu: "4"
              requests.memory: 4Gi
              limits.cpu: "5"
              limits.memory: 4Gi
          ```
    - Policy
    - Allow resource to connect with each other with DNS.
- Namespace:
    - Default
    - kube-system
    - kube-public
- Namespace Isolation
    - Dev
    - Prod
- DNS:
    - "db-service.prod.svc.cluster.local":
        - Service Name: db-service
        - Namespace: prod
        - Service: svc
        - Domain: cluster.local
- `--namespace=<namespace>`:
    - default: Default
- Assign a Namespace when you create a new resource:
   - ```yaml
      apiVersion: v1
      kind: Pod
      metadata:
        name: app-pod
        namespace: prod
      ....
      ``` 
- Create a new namespace
    - By YAML:  
      ```yaml
      apiVersion: v1 
      kind: Namespace
      metadata:
        name: prod
      ```
    - By command line: `kubectl create namespace prod`
- Set namespace:
    - `kubectl config set-context $(kubectl config current-context) --namespace=prod`
- Get resources in all namespaces:
    - `kubectl get all --all-namespaces`
