# 6. Istio Gateway

## Why we need Istio Gateway?
- Because the proxies run after a container makes a request, so if users access a specific pod directly, you can't use routing.
    - Without Ingress Gateway:
    ```
    web -> pod A
    web -> pod B
    ```
    - With Ingress Gateway (Edge Proxy):
    ```
    web -> Istion Gateway (pod -> proxy) -> proxy A (80%) -> pod A
                                         -> proxy B (20%) -> pod B
    ```
- Type:
    - Default: LoadBalancer
- [Configuring ingress using an Istio gateway](https://istio.io/latest/docs/tasks/traffic-management/ingress/ingress-control/)
- Note:
    You can restirct the request to specific hosts by adding hosts in spec:
    ```yaml
    apiVersion: networking.istio.io/v1alhpa3
    kind: Gateway
    metadata:
      name: ingress-gateway-configuration // default isiot gateway
    spec:
      selector:
        istio: ingressgateway
      servers:
      - port:
          number: 80
          name: http
          protocol: HTTP
        hosts:
        - test.example.com
    ```
## Advanced 
- Prefixing Routing
    - HttpRequestMatch
        - uri:
            - exact
            - prefix
            - regex
                - example:
                  ```yaml
                  spec:
                    - match:
                      - uri: # if
                          prefix: "/test1"
                      - uri: # or
                          prefix: "/test2"
                      route: # then
                      - destination:
                            host: app1
                            subset: test
                    - match:
                      - uri:
                          prefix: "/"
                      route:
                      - destination:
                          host: app2
                          subset: origin
                  ```
        - Headers
            - exact
                - example:
                  ```yaml
                  http:
                    - match:
                       - headers
                           hederOne:
                             exact: test1
                       route:
                       - destination:
                           host: test1-myweb
                           subset: test1
                    - route: # catch all
                       - destination:
                           host: default-myweb
                           subset: default
                  ```
            - prefix
            - regex
        - Reference: [HTTPMatchRequest](https://istio.io/latest/docs/reference/config/networking/virtual-service/#HTTPMatchRequest)
- Subdomain Routing 
    ```
    apiVersion: networing.istio.io/v1alpha3
    kind: Gateway
    metadata:
      name: ingress-gateway-configuration 
    spec:
      selector:
        istio: ingressgateway
      servers:
      - port:
          number: 80
          name: http
          protocol: HTTP
      
        host:
        - "*.myweb.com"
    --- 
    kind: VirtualService
    apiVersion: networking.istio.io/v1alpha3
    metadata:
      name: mywebapp
      namespace
    spec:
      hosts:
        - "test1.myweb.com"
      gateways:
        - ingress-gateway-configuration 
      http:
         - route:
           - destination:
               host: web1
               subset: test1
    ```
