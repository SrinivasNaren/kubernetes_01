
# **1️⃣ Folder Structure**

```
minikube-nginx-demo/
├── README.md
├── pod/
│   └── nginx-pod.yaml
├── service/
│   └── nginx-svc.yaml
└── notes/
    └── commands.txt
```

**Explanation:**

* `pod/` → contains pod YAML files.
* `service/` → contains service YAML files.
* `notes/` → contains useful commands you used during setup.
* `README.md` → detailed guide for anyone to replicate your setup.

---

# **2️⃣ Pod YAML (`pod/nginx-pod.yaml`)**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
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

# **3️⃣ Service YAML (`service/nginx-svc.yaml`)**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  selector:
    app: nginx
  type: NodePort
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

---

# **4️⃣ Notes (`notes/commands.txt`)**

```
# Start Minikube
minikube start --driver=docker --kubernetes-version=v1.33.1

# Check status
minikube status
kubectl get nodes
kubectl get pods -A

# Create pod
kubectl apply -f pod/nginx-pod.yaml
kubectl get pods --show-labels

# Expose pod
kubectl apply -f service/nginx-svc.yaml
kubectl get svc

# Access service URL
minikube service nginx

# Exec into pod
kubectl exec -it nginx -- /bin/bash
exit
```

---

# **5️⃣ README.md**

```markdown
# Minikube Nginx Demo

This repository demonstrates a **simple Nginx Pod and Service running on Minikube**.  
It includes the pod and service YAML files and a list of commands to manage Kubernetes resources.

## Prerequisites

- Minikube installed (Windows/Linux)
- Docker installed and running
- kubectl installed

## Folder Structure

```

minikube-nginx-demo/
├── README.md
├── pod/
│   └── nginx-pod.yaml
├── service/
│   └── nginx-svc.yaml
└── notes/
└── commands.txt

````

## Steps

1. **Start Minikube**

```bash
minikube start --driver=docker --kubernetes-version=v1.33.1
````

2. **Deploy Nginx Pod**

```bash
kubectl apply -f pod/nginx-pod.yaml
kubectl get pods --show-labels
```

3. **Expose Pod as NodePort Service**

```bash
kubectl apply -f service/nginx-svc.yaml
kubectl get svc
```

4. **Access the Service**

```bash
minikube service nginx
```

5. **Optional: Exec into Pod**

```bash
kubectl exec -it nginx -- /bin/bash
```

6. **Stop & Delete Minikube**

```bash
minikube delete --all --purge
```

## Notes

* Pod must have **labels** for services to route traffic.
* NodePort exposes the service outside the cluster.
* YAML files can be version controlled and reused.

