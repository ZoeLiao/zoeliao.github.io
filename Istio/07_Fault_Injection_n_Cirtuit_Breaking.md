# 07 Fault Injection, Cirtuit Breaking

You can use it to do [Chaose Engineering](https://en.wikipedia.org/wiki/Chaos_engineering)

## Fault Injection
### Virtual Service
-  HttpFaultInjection:
    - Abot
    - Delay
    ```yaml
    fault:
      delay:
        percentage:
          value: 100.0
        fixedDelay: 5s
    ```

## Circut Breaking
### [Cascading Failures (級聯故障)](https://en.wikipedia.org/wiki/Cascading_failure)
- A cascading failure is a process in a system of interconnected parts in which the failure of one or few parts can trigger the failure of other parts and so on. Such a failure may happen in many types of systems, including power transmission, computer networking, finance, transportation systems, organisms, the human body, and ecosystems.
- How to solve this?
    - [Circuit Breaker](https://en.wikipedia.org/wiki/Circuit_breaker_design_pattern)
        - Monitor the successful requests are making. If the request is failed it will cut the connection.
        - e.g., [Hystrix (No Development)](https://github.com/Netflix/Hystrix)
- How to do Circuit Breaking in Istio? No need to modify application
```
Microservice -> Proxy  (Circuit Breaker) - 50% -> Pod a (503)
                                         - 50% -> Pod b
```
```
Microservice -> Proxy  (Circuit Breaker) - X -> Pod a (No request)
                                         - 100% -> Pod b
(Remove Pod a from load balancing)
```
- [Backpressure](https://medium.com/@jayphelps/backpressure-explained-the-flow-of-data-through-software-2350b3e77ce7):
    - Resistance or force opposing the desired flow of data through software.
- The Risk of Circuit Breaking
    - If you do not set it well, you will trigger it everytime.


### Configuring Outlier Detection
- Traffic Management:
    - Destination Rule:
        - Outlier detection (Circuit Breaker)
        - default: triggered by 502, 503, 504 only
        - consecutive5xxErrors: any 5xx Errors
        ```yaml
        apiVersion: networking.istio.io/v1alpha3
        kind: DestinationRule
        metadata:
          name: my-circuit-breaker
        spec:
          host: my-service.default.svc.cluster.local
          trafficPolicy: // triggered by 502, 503, 504 only
            outlierDetection:
              consecutiveErrors: 3
              interval: 10s
              baseEjectionTime: 35s // minimum ejection time, i.e., how long the pod will be removed
        ```
        - [Ejection algorithm](https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/upstream/outlier)

