# State Persistence

## Volumn
- Attach a volumn to a pod can retain data created by the pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myweb
spec:
  containers:
  - image: alpine
    name: alpine
    command: ["/bin/sh", "-c"]
    args: ["echo 123 >> /opt/number.out"]
    volumeMounts:
    - mountPath: /opt
      name: myVolume

volumes:
- name: myVolume
  hostPath:
    path: /data
    type: Directory
```

## Type
- HostPath: is not recommended for multiple nodes
- Others: EBS, EFS, NFS, GlusterFS, Ceph, Scaleio
```yaml
volumes:
- name: myVolume
  awsElasticBlockStore:
    volumeID: <volume_id>
    fsType: ext4
```

## Persistent Volumn
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-vol
spec:
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 1Gi
  awsElasticBlockStore:
    volumeID: <volume_id>
    fsType: ext4
```
- create: `kubectl create -f pv.yaml`
- get: `kubectl get persistentvolume`

## Persisitent Volume Claim (PVC)
- Kubernetes bind a PVC to a PV (1 to 1 releationship)
- Settings:
    - Sufficient Capacity
    - Access Modes
    - Volume Mode
    - Storage Class
    - Selector
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pv-claim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
        storage: 500Mi
  persistentVolumeReclaimPolicy: retain
```
- create: `kubectl create -f pvc.yaml`
- get: `kubectl get persistentvolumeclaim`
- delete: `kubectl get persistentvolumeclaim pv-claim`

## Storage Classes
- Static Provisioning: storage is created manually
- Dynamic Provisioning: create by cloud and attach to PV
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
    name: google-storage
provisioner: kubernetes.io/gce-pd
parameters:
    type: pd-standaer
    replication-type: none
```
- Add StorageClassess in PVC:
```yaml
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: google-storage
```

## Stateful Sets
- Why we need it?
    - order: e.g., Set up master db first and then slaves
```yaml
kind: StatefulSets
```
- create: `kubectl create -f statefulset.yaml`
- scale: `kubectl scale statefulset mysql --replicase=5`
- delete:  `kubectl delete statefulset mysql`

### Pod policy
- You can decide manage pod in order or paralelly

### Headless services
- Services:
    - DNS: e.g., mysql.default.svc.cluster.local
    - Load traffic to pod
    - The IP of pod is dynamic
- Headless services:
    - There is no IP, each pod has dns, e.g., mysql-0.mysql-h.default.svc.cluster.local
```yaml
apiVersion: v1
kindL Service
metadata:
  name: mysql-h
spce:
  ports:
    - port: 3306
  selector:
    app: mysql
  clusterIP: None <-- set this
```
pod:
```
subdomain: mysql-h
hostname: mysql-pod <-- A record for all 
```


