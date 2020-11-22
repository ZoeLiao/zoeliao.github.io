# Label, Selector, Annotation

## Labels & Selectors
- Lables: properties attached to each item. Take the following pod.yaml for example:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
  labels:
    app: web
    env: prod
```
- Selectors: Filters for labels.
- You can use labels and selectors to group objects.
- Command: `kubectl get pods --selector env=prod`
- Example: replicaSet:
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: webapp
  labels:
    app: frontend
    env: prod
spec:
  replicas: 3
  selector:
    matchLabels:
      app: frontend <- match pod's label
    template:
      metadata:
        labels:
          app: frontend
          env: prod
    spec:
      containers:
      - name: myweb
        image: myweb
```

## Annotations:
- Record details, e.g., version, for intergration purpose.
