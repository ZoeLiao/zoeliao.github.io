# Multi-container Pod

- Have multi-cotainers in a pod.
- Share the same lifecycle, network and storage
- pod.yaml:
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: mywebapp
      labels:
        name: mywebapp
    spec:
      containers:
      - name: mywebapp
        image: mywebapp
        ports:
          containerPort: 8080
      - name: mylog
        image: mylog
        ports:
          containerPort: 8081
    ```

## Pattern
- Sidecar:
    log -> log server
- Adapter: 
    convert multi-format logs into a same format -> log server 
- Ambassdor:
    outsource logic to a container to send logs to different databases (dev, staging, prod)



