# Rolling Updated & Rollbacks

## The commands of deployment
### Create
- kubectl create:
    - `kubectl create -f <deployment_file>.yaml` 
- kubectl run:
    - `kubectl run <deployment_name> --image=<image_name>`

### Get
- `kubectl get deployments`

### Update
- `kubectl apply -f <deployment_file>.yaml`
- `kubectl set image deployment/<deployment_name> key=value`: the file is unchanged.
- How it works?
    - destory the old replica-set
    - create a new replica-set

### Check Status
- `kubectl rollout status deployment/<deployment_name>`
- `kubectl rollout history deployment/<deployment_name> --version=<version>`

### Rollout
- When you create a deployment, it trigger a rollout, and it create a revision.
- `kubectl rollout status deployment/<deployment_name>`
- Deployment Strategy:
    - Recreate: Destroy all of the all versions  -> application down -> create new version
    - Rolling Update: Deafult. Destory and create pod one by one, so that the application will keep running if you have more than one pod. 
- If the new pod is unvailable, k8s will not terminate the old one.

### Rollback
- Command line: `kubectl rollout undo deployment/<deployment_name>`
- How it works?
    - Destory the new replica-set
    - create the old replica-set
