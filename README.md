

# 🐳 Kubernetes Practice Repo

**Practice Kubernetes core concepts: Pods, ReplicaSets, and Deployments.**

---

## 📂 Contents

| Folder         | File                    | Description                                         |
| -------------- | ----------------------- | --------------------------------------------------- |
| `pods/`        | `nginx-pod.yaml`        | Basic Pod definition                                |
| `replicasets/` | `nginx-replicaset.yaml` | ReplicaSet to manage multiple Pods                  |
| `deployments/` | `nginx-deployment.yaml` | Deployment managing ReplicaSet with rolling updates |

---

## 📌 Key Concepts

### **Pod**

* Smallest deployable unit in Kubernetes.
* Runs **one or more containers**.
* YAML defines **container image, ports**, and other configs.

```yaml
apiVersion: v1        # Kubernetes API version
kind: Pod             # Object type
metadata:
  name: nginx-pod     # Pod name
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
```

---

### **ReplicaSet**

* Ensures a **fixed number of identical Pods** are running.
* Self-healing: replaces **crashed Pods** automatically.
* **Selector labels** must match Pod template.

```yaml
replicas: 3               # Always 3 Pods
selector:
  matchLabels:
    app: nginx            # Select Pods to manage
template:
  metadata:
    labels:
      app: nginx
  spec:
    containers:
    - name: nginx
      image: nginx:latest
      ports:
      - containerPort: 80
```

---

### **Deployment**

* Manages **ReplicaSets**.
* Adds **rolling updates, rollback**, and versioned history.
* Deployment → ReplicaSets → Pods.

```yaml
replicas: 3
selector:
  matchLabels:
    app: nginx
template:
  metadata:
    labels:
      app: nginx
  spec:
    containers:
    - name: nginx
      image: nginx:latest
      ports:
      - containerPort: 80
```

---

## ⚡ Commands to Practice

### **Pod**

```bash
kubectl apply -f pods/nginx-pod.yaml
kubectl get pods
kubectl describe pod nginx-pod
kubectl delete pod nginx-pod
```

### **ReplicaSet**

```bash
kubectl apply -f replicasets/nginx-replicaset.yaml
kubectl get rs
kubectl get pods -l app=nginx
kubectl delete pod -l app=nginx --field-selector=status.phase=Running
```

### **Deployment**

```bash
kubectl apply -f deployments/nginx-deployment.yaml
kubectl get deployments
kubectl get pods -l app=nginx
kubectl rollout status deployment/nginx-deployment
kubectl rollout undo deployment/nginx-deployment
```

---

## 📖 Notes

* Always ensure **labels and selectors match**.
* Use **resources** in containers to avoid noisy neighbor issues.
* Use **rollout undo** to rollback bad updates in Deployments.
