# Ingress

## How to
- Deploy (Not deployed by default):
    - Ingress Controller:
        - NGINX
        - Haproxy
        - traefik
        - Istio
        - GCE (GCP HTTP(s) Load Balancer)
    - Deployment:
    ```yaml
    apiVersion: extensions/v1betal
    kind: Deployment
    metadata:
      name: nginx-ingress-controller
    spec:
      replicas: 1
      selector:
        matchLabels:
          name: nginx-ingress
        template:
          metadata:
            labels:
              name: nginx-ingress
          spec:
            containers:
              - name: nginx-ingress-controller
                image: quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.21.0
            agrs:
              - /nginx-ingress-controller
              - --configmap=$(POD_NAMESPACE)/nginx-configuration
            env:
              - name: POD_NAME              
                valueFrom:
                  fieldRef:
                    fieldPath: metadata.name
              - name: POD_NAMESPACE
                valueFrom:
                  fieldRef:
                    fieldPath: metadata.namespace
            ports:
              - name: http
                containerPort: 80
              - name: https
                containerPort: 443
    ```
    - ConfigMap: you should write a configMap to store: 
        - err-log-path
        - keep-alive
        - ssl-protocols
    ```yaml
    kind: ConfigMap
    apiVersion: v1
    metadata:
      name: nginx-configuration
    ```
    - Service:
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: nginx-ingress
    spec:
      type: NodePort
      ports:
      - port: 80
        targetPort: 80
        protocol: TCP
        name: http
      - port: 443
        targetPort: 443
        protocol: TCP
        name: https
    selector:
      name: nginx-ingress
    ```
    - Auth - ServiceAccount
    ```yaml
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: nginx-ingress-serviceaccount
    ```
- Ingress Resources:
    - Set rules to route traffics to a specific service
    ```yaml
    apiVersion: extensions/v1beta1
    kind: Ingress
    metadata:
      name: ingress-wear
    spec:
      rules:
      - host: host1.com
        http:
        paths:
        - path: /homepage  
            backend:
              serviceName: main-service
              servicePort: 80
      - host: host2.com
        http:
        - path: /watch 
            backend:
              serviceName: watch-service
              servicePort: 80
    ```
    - Default backend: if the request does not match nay rules, it will bre redirect to the default backend.
