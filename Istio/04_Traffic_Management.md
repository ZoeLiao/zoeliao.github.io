# 04. Traffic Management

## Canary Release
- Deploy a new version of a software component but only make that new image live for a percentage of the time.
- The working version is the one being used in most of the time.

### k8s
- You can copy the old deployment and rename it to use Canary Release.

### Istio
- It allow you to do Canary Release by Version Grouping & Weighted Routing without mdofiying any code:
    - Use version to do deploy different deployments.
    - Then click "Create Weighted Routing" to do Canary Release.
    - The request will be redirected to the new deployments randomly.
- Virtual Service
    - `kubectl get vs`
    - enables you to conigure custom routing rules to the service mesh. 
    - In k8s, a service is for service discovery. It is to automatically manange DNS service.
    - In Istio, VirtulaService managed by Istio-pilot to overwirte the Envoy proxy configuration.
    - ```yaml
      kind: VirtualService
      apiVersion: networking.istio.io/v1alpha3
      metadata:
        name: test # name of virtual service
        namespace: default # the namespace of target serviCe
      spec:
        hosts:
          - mytest-domain.default.svc.cluster.local // the service DNS (k8s service)name
        http:
          - route:
             - destination:
                 host: mytest-domain.default.svc.cluster.local // the target DNS name
                 subset: a
               weight: 20
             - destination:
                 host: mytest-domain.default.svc.cluster.local // the target DNS name
                 subset: b
               weight: 80
      ```

- Destination Rules
    - `kubectl get dr`
    - ```yaml
      kind: DestinationRule # Define which pods shuold be part of each subsets
      apiVersion: networking.istio.io
      metadata:
        name: my-service
        namespace: default
      spec:
        host: my-service
        trafficPolicy:
        subsets:
          - labels: # selectors
              version: a
            name: a
          - labels:
              version: b
            name: b
      ```
    - A configuration for load balancer to a particular service.

- Kiali will validate your yaml, but you can only delete all traffic routing/
