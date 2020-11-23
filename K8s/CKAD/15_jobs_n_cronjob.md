# Job

## Types of Workloads
- Running for long time:
    - web
    - application
    - database
- Running for a short period of time:
    - data processing
    - analysis

## Policy
- RestartPolicy:
    - Never
    - Always

## K8s Jobs
- completions: the numbers of pods, new pod will be created after the prvious pod is completed.
- parallelism: create in parall
- Default:
    - Number: 1.
    - If you don't set completion, the default is parallelism
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: pi
spec:
  completions: 3
  parallelism: 3
  template: <-- pod.yaml
    spec:
      containers:
      - name: pi
        image: perl
        command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
  backoffLimit: 4
```
- Create: `kubectl create -f <job_file>.yaml`
- Get:
    - `kubectl get jobs`
    - `kubectl get pods`
- Check: `kubectl logs <job_name>` 
- Delete: `kubectl delete job <job_name>`
- If new pod is failed, it will keep create a new one untill three times. 

## CronJob
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: pi
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      completions: 3
      parallelism: 3
      template:
        spec:
          containers:
          - name: pi
            image: perl
            command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
          restartPolicy: Never
      backoffLimit: 4
```
