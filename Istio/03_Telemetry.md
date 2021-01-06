# 3. Telemetry

## Requirements
- 1. Need a Proxy (Envoy Sidecar) running in each pod you want to monitor.
- 2. The control plane needs to be running (ie istiod, kiali, jaeger, and grafana).
- 3. You do not need any specific Istio yaml configuration. 
(No need for VirtualServices, Gateway, etc)
