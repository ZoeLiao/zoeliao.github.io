# Service Account

## Account
- User Account: used by user, e.g., admin, developer
- Service Account: used by machine, e.g., Jenkins, Prometheus

## Service Account
- Create: `kubectl create serviceaccount <service account name>`
    - Create object
    - Create a token
    - Create a secret to store the token
    - You can use the token to run K8s API query
- Each namespace has its own default service account.
- automountServiceAccountToken:
    - value: true/false 
    - level: pod
