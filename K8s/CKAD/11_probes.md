# Probe

## Live Cycle
Pod Status:
- pending: k8s is finding a suitable node to schedulet the pod
- containerCreating: the pod has been scheduled on a node and it is creating container(s).
- Running
- Terminate

Conditions:
- PodScheduled 
- Initialized
- ContainersReady
- Ready: is ready to accept request

## Readiness Probes
- Ready:
    - Default: Once a container is created, it is ready to accept traffic
    - Custom: Use readiness probes to check whether the application is ready or not.
        - Type:
            - httpGet
            - tcpSocket
            - command
        - More settings:
            - initialDelaySecondes
            - periodsSeconds
            - failureThreshold

pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myweb
  labels:
    name: myweb

spec
  containers:
    - name: mycontainer
      image: mycontainer
      ports:
        - containerPort: 8080
      readinessProbe:
        httpGet:
          path: /index.html
          port: 8080
```

---

## Liveness Probes
- If a pod is crashed, k8s will keep restart it. However, if a web application within the pod is crashed, we need to use liveness probes to check and create a new pod.
- The type and more settings is the same as readinessProbe.

pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myweb
  labels:
    name: myweb

spec
  containers:
    - name: mycontainer
      image: mycontainer
      ports:
        - containerPort: 8080
      livenessProbe:
        httpGet:
          path: /index.html
          port: 8080
```
