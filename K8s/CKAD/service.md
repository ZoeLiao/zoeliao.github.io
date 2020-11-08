# Services

## Types
- NodePort
    - ports:
        - target port: the port of pod. 
        - Port: the port of service.
        - Nodeport: the port of node. range: 30000 ~ 32767
    ```yaml
      apiVersion: v1
      kind: Service
      metadta:
        name: app-service
      spec:
        type: NodePort
        ports:
        - targetPort: 80
          port: 80 <-- if you don't write it, it will be the same as the targetPort
          nodePort: 30000
        selector: <-- there are lots of pod in the node, we need to select a specific pod by label
          app: app
          type: front-end
    ```
    - Support to load requests randomly to:
        - a single pod on a single node
        - multiple pods on a single node
        - multiple pods on multiple nodes
- ClusterIP
    - Allow users to connect to multiple pods by a single endpoint
    - ```yaml
      apiVersion: v1
      kind: Service
      metadta:
        name: app-service
      spec:
        type: ClusterIP <-- default
        ports:
        - targetPort: 80
          port: 80
        selector: <-- there are lots of pod in the node, we need to select a specific pod by label
          app: app
          type: front-end
      ```
    
- LoadBalancer
