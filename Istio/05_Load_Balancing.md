# 5. Load Balancing

## TrafficPolicy
- You can modify the trafficPolicy of Destination Rule to make sticky session.
```yaml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: my_web
spec:
  host: my_web.staging.svc.cluster.local
  trafficPolicy:
    loadBalancer:
     consistentHash:
        useSourceIp: true
```
- Load balancer
    - Typically algorithm: round robin (輪詢)
    - Consistent hashing:
        - Source IP -> Hash
        - You do some heavy processing for a user, and you want to cache that in the pod's memory so the next time the same client requests, they get a cache hit. Don't ever rely on this to implement a "session".
    - You can use:
        - httpHeaderName: you need to make sure the header will be propagated during the whole Jeager trace.
        - httpCookie
        - useSourceIp
        - minimumRingSize
- But if you want to use it with weighting routing, it does not work.
