# 🚀 Microservices Notes App

## Project Structure
```
microservices-app/
├── backend/
│   ├── server.js        # Node.js API
│   ├── package.json
│   └── Dockerfile       # Multi-stage build
├── frontend/
│   ├── index.html       # UI
│   ├── nginx.conf       # Nginx config (API proxy)
│   └── Dockerfile
├── k8s/
│   └── deployment.yaml  # Sabhi K8s resources
├── Jenkinsfile          # CI/CD Pipeline
└── README.md
```

---

## ⚙️ Setup Steps

### Step 1 — deployment.yaml mein apna DockerHub username daalo
```yaml
image: YOUR_DOCKERHUB_USERNAME/microservices-backend:latest
image: YOUR_DOCKERHUB_USERNAME/microservices-frontend:latest
```

### Step 2 — Jenkinsfile mein username daalo
```groovy
DOCKERHUB_USERNAME = 'YOUR_DOCKERHUB_USERNAME'
```

### Step 3 — Namespace banao aur deploy karo
```bash
kubectl apply -f k8s/deployment.yaml
```

### Step 4 — Verify karo
```bash
kubectl get all -n microservices
```

### Step 5 — Ingress setup karo
```bash
# Minikube tunnel chalao
sudo minikube tunnel

# Hosts file mein add karo
sudo nano /etc/hosts
# 127.0.0.1  microservices.local
```

### Step 6 — Browser mein open karo
```
http://microservices.local
```

---

## 🔥 Jenkins Pipeline Steps
1. Git Clone
2. Build Backend Image
3. Build Frontend Image
4. Push to DockerHub
5. Deploy to Kubernetes
6. Verify Deployment
7. Health Check
8. Auto Rollback on Failure

---

## 📌 Important Commands
```bash
# Sabhi pods dekho
kubectl get pods -n microservices

# Logs dekho
kubectl logs -l app=backend -n microservices
kubectl logs -l app=frontend -n microservices

# HPA dekho
kubectl get hpa -n microservices -w

# Rollback karo
kubectl rollout undo deployment/backend-deployment -n microservices

# Delete everything
kubectl delete namespace microservices
```
