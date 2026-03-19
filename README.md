MERN-Stack Todo Application with Kubernetes
This project demonstrates a containerized MERN (MongoDB, Express, React, Node.js) application deployed on a Kubernetes cluster with Persistent Storage and Horizontal Pod Autoscaling (HPA).

**🛠 Tools and Technologies**
Frontend: React.js

Backend: Node.js & Express.js

Database: MongoDB

Containerization: Docker & Docker Compose

Orchestration: Kubernetes (Minikube)

Monitoring: Metrics Server

**🏗 Application Architecture**
The application is split into three main tiers:

Web Tier: React frontend pods managed by a Deployment and exposed via a NodePort/LoadBalancer service.

API Tier: Node.js backend pods with Resource Limits (CPU) and Auto-scaling enabled.

Data Tier: MongoDB pod attached to a Persistent Volume Claim (PVC) to ensure data survives pod restarts.

**🐳 Docker Instructions**
Build Images
# Build Backend Image
docker build -t todobackend:latest ./backend

# Build Frontend Image
docker build -t todofrontend:latest ./frontend
Run with Docker Compose
# Start the entire stack locally
docker-compose up -d
**☸️ Kubernetes Deployment Steps**
**1. Environment Setup**
minikube start
minikube addons enable metrics-server
minikube image load todobackend:latest
minikube image load todofrontend:latest
**2. Deploy Infrastructure (Storage & Database)**
kubectl apply -f k8s/mongo-pvc.yaml
kubectl apply -f k8s/mongodb-deployment.yaml
**3. Deploy Application Services**
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/frontend-deployment.yaml
**4. Access the App**
minikube service frontend-service

**Bash**
minikube service frontend-service
**📈 Scaling Configuration (Task 5)**
The backend is configured to scale automatically based on CPU utilization.

Metric: CPU Utilization

Target Threshold: 70%

Minimum Replicas: 2

Maximum Replicas: 5

Apply HPA Policy:
kubectl apply -f k8s/backend-hpa.yaml
**Verify Scaling Status:
kubectl get hpa
Verification Proof
Persistence: Data stored in MongoDB remains available even after deleting the database pod.

Scaling: New pods are automatically provisioned when CPU limits are reached and scaled down to 2 during idle periods.**
