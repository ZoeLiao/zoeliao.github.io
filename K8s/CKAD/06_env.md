# env

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
  containers:
    - name: app-pod
      image: app-pod
      ports:
        - contaierPort: 80
      env:
      - name: DB_NAME
        value: mysql 
```

## Type
- plain key value
    ```yaml
    env:
    - name: DB_NAME
      value: mysql 
    ```
- configMap
    - Create a configMap:
        - Imperative way: `kubectl create configmap`
            - from literal:
            ```bash
            kubectl create configmap \
            <config_name> --from-literal=<key>=<value>`
            ```
            - from file:
            ```bash
            kubectl create configmap \
            <config_name> --from-file=<path-to-file>`
            ```
        - Declarative way: `kubectl create -f`
        ```yaml
        apiVersion: v1
        kind: ConfigMap
        metadata:
          name: app-config
        data:
          DB_NAME: mysql 
          ENV: prod
        ```
    - ConfigMap in Pod: 
    ```yaml
    env:
    - name: DB_NAME
      valueFrom:
          configMapKeyRef
    ```
    - Command:
        - Get: `kubectl get configmaps` 
        - Describe: `kubectl describe configmaps` 
- secret
    - Create a secret:
        - Imperative way: `kubectl create secret generic`
            - from literal:
            ```bash
            kubectl create secret generic\
            <config_name> --from-literal=<key>=<value>`
            ```
            - from file:
            ```bash
            kubectl create secret generic\
            <config_name> --from-file=<path-to-file>`
            ```
        - Declarative way: `kubectl create -f`
            - Convert data into hash:
            ```bash
            echo -n "pwd" | base64
            ```
            - Put hash into yaml
            ```yaml
            apiVersion: v1
            kind: secret
            metadata:
              name: app-secret
            data:
              DB_Host: <hash> 
              DB_User: <hash>
              DB_Password: <hash>
            ```
    - Secret in Pod: 
        ```yaml
        env:
        - name: DB_Host
        valueFrom:
          secretKeyRef
        ```
    - Command:
        - Get: `kubectl get secrets` 
        - Describe: `kubectl describe secrets` 
        - To yaml: `kubectl get secret <secret_name> -o yaml`
        - Decode hash:
        ```bash
        echo -n "<hash>" | base64 --decode
        ```
- Security Context
    - You can write in pod or container level.
    - Priority: container > pod
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: pod
    spec:
      securityContext: <-- pod level
        runAsUser: 1000
      containers:
          - name: ubuntu
            image: ubuntu
            command: ["echo", "hi"]
              securityContext: <-- container level
                runAsUser: 1000
                capabilities:  <-- container level only
                    add: ["MAC_ADMIN"] 
    ```
