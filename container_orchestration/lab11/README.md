# Lab 11: Namespace Management and Resource Quota Enforcement

## Objective
Create a dedicated namespace, apply a `ResourceQuota` that caps the namespace to
2 pods, and confirm the cluster actually enforces that limit by trying to exceed it.

## Steps & Commands

### 1. Create the ivolve namespace
```bash
kubectl create namespace ivolve
```
![create namespace](screenshots/create_namespace.png)

Verify it:
```bash
kubectl get namespaces
```
![verify namespace](screenshots/verify_namespace.png)

### 2. Apply the resource quota
`resource-quota.yaml`:
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: pod-quota
  namespace: ivolve
spec:
  hard:
    pods: "2"
```

```bash
kubectl apply -f resource-quota.yaml
```
![apply quota](screenshots/apply_quota.png)

### 3. Verify the quota is in place
```bash
kubectl describe resourcequota pod-quota -n ivolve
```
![describe quota](screenshots/describe_quota.png)

Or a quick summary:
```bash
kubectl get resourcequota -n ivolve
```
![get quota](screenshots/get_quota.png)

### 4. Prove enforcement — try to exceed the limit
`test-deployment.yaml` requests 3 replicas, one more than the quota allows:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: quota-test
  namespace: ivolve
spec:
  replicas: 3
  selector:
    matchLabels:
      app: quota-test
  template:
    metadata:
      labels:
        app: quota-test
    spec:
      containers:
        - name: nginx
          image: nginx:alpine
```

```bash
kubectl apply -f test-deployment.yaml
```
![apply test deployment](screenshots/apply_test_deployment.png)

Check what actually came up:
```bash
kubectl get pods -n ivolve
```
![pods enforcement](screenshots/pods_enforcement.png)

Expect to see only **2** pods running.

## Project Structure
```
lab11/
│
├── resource-quota.yaml
├── test-deployment.yaml
└── README.md
```