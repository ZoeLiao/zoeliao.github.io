# Deployment

## Upgrade
- rolling upgrade

- Deployment
    - Replica Set

## Definition
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-deployment
  labels:
      app: app
      type: front-end
spec:
  template:
    metadata:
      name: app-pod
      type: front-end
    spec:
      containers:
      - name: nginx-container
        image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: front-end
```
- Create: `kubectl create -f deployment.yaml` 
- Get all: `kubectl get all`
    - or:
        - Get Deployments: `kubectl get deployments`
        - Get Replicaset: `kubectl get replicaset` 
        - Get Pods: `kubectl get pods`

## Others
- `--dry-run`: tell you whether the resource can be created and if your command is right instead of creating the resource.
- `-o <option>`:
    - `-o yaml`: This will output the resource definition in YAML format on the screen.
    - `-o json`: This will output the resource definition in json format on the screen.
    - `-o name`: Print only the resource name and nothing else. 
    - `-o wide`: Output in the plain-text format with any additional information.

