# Select Node

## Taints and Tolerations
- If a node is tainted, only the pod which has required toleration can be scheduled on this node.
- Master node is tainted so that no pod can be scheduled on it.


### Taint
- Object: node 
- Key workds:
    - key, e.g., app
    - value, e.g., myweb
    - taint effect
        - 1. Noschedule: a pod will not be scheduled on the tainted node.
        - 2. PreferNoSchedule: k8s will try to avoid to schedule a pod on a node but it is not guartenteed.
        - 3. NoExecute: new pods will not be scheduled on the node, and for what has been scheduled on the node will be removed.
- command: `kubectl taint nodes <node_name> key=value:taint-effect`, e.g., `kubectl taint nodes mynode app=myweb:NoExecute`

### Toleration
- Object: pod
- key words:
- yaml: e.g., pod.yaml
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: myapp
  spec:
    containers:
      name: myapp
     
    tolerations:
    - key: "app" 
      operator: "Equal"
      value: "taintedNode" 
      effect: "NoSchedule"
  ```

## Node Selectors
- Make a pod be scheduled on a specific node.

### How
- Label a Node:
    - Command line: `kubectl label nodes <node_name> <label_key>=<label_value>`, e.g., `kubectl label nodes mynode size=small`

- Selcet the Node by label:
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: myapp
  spec:
    containers:
    - name: mycontainer
      image: mycontainer
    nodeSelector:
      size: small
  ```
- If you want to select nodes in a more comlicated situation, use affinity instead. 

## Affinity
- Ensure a pod be scheduled on a specific node.

### Types
- Available:
    - requiredDuringSchedulingIgnoredDuringExecution
    - peferredDuringSchedulingIgnoredDuringExecution
- Planned:
    - requiredDuringSchedulingRequiredDuringExecution

- yaml:
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: myapp
  spec:
    containers:
    - name: mycontainer
      image: mycontainer
    affinity:
      nodeAffinity:
        requiredDuringSchedulingIgnoreDuringExecution:
          nodeSelectorTrems:
          - matchExpressions:
            - key: size
              operator: In
              values:
              - Small
  ```
