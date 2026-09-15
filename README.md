# Kubernetes Node.js Application

A hands-on Kubernetes project demonstrating how to containerize and deploy a Node.js application using Kubernetes. The project covers Deployments, Pods, ConfigMaps, Secrets, Persistent Volumes, Persistent Volume Claims, scaling, rolling updates, and Kubernetes self-healing.

## 🚀 Project Overview

This project demonstrates a complete basic Kubernetes deployment workflow:

- Node.js application
- Docker containerization
- Kubernetes Deployment
- Multiple replicas
- ConfigMap for configuration
- Secret for sensitive values
- PersistentVolume (PV)
- PersistentVolumeClaim (PVC)
- Persistent storage mounted inside Pods
- Application scaling
- Rolling updates
- Kubernetes self-healing
- Git and GitHub version control

## 🛠️ Technologies Used

- Node.js
- Docker
- Kubernetes
- kubectl
- YAML
- Git
- GitHub

## 📁 Project Structure

```text
kubernetes-project/
│
├── app/
│   ├── package.json
│   ├── package-lock.json
│   ├── server.js
│   └── Dockerfile
│
├── k8s/
│   ├── deployment.yaml
│   ├── configmap.yaml
│   ├── secret.yaml
│   ├── pv.yaml
│   └── pvc.yaml
│
├── .gitignore
└── README.md
🐳 Docker Image
The Node.js application is containerized using Docker.
Example image:
kubernetes-node-app:2.0
The application runs on port:
3000
☸️ Kubernetes Components
1. Deployment
The Kubernetes Deployment manages the application Pods.
It provides:
Desired number of replicas
Pod management
Rolling updates
Automatic replacement of failed Pods
Example:
apiVersion: apps/v1
kind: Deployment
metadata:
  name: node-app
The application can be scaled using:
kubectl scale deployment node-app --replicas=4
Check the Pods:
kubectl get pods
2. ConfigMap
The project uses a ConfigMap named:
node-app-config
ConfigMaps are used to store non-sensitive configuration values separately from the application code.
The Deployment loads these values using:
envFrom:
  - configMapRef:
      name: node-app-config
3. Secret
Sensitive configuration is stored in a Kubernetes Secret:
node-app-secret
The application uses Secret values such as:
API_KEY
DB_PASSWORD
The Secret is injected into the container using:
envFrom:
  - secretRef:
      name: node-app-secret
Never commit real secrets, passwords, or API keys to GitHub.
💾 4. Persistent Storage
The project demonstrates Kubernetes persistent storage using:
PersistentVolume
node-app-pv
Capacity:
1Gi
Access mode:
ReadWriteOnce
PersistentVolumeClaim
node-app-pvc
Requested storage:
500Mi
The storage is mounted inside the application container at:
/app/data
Example:
echo "Hello from persistent storage" > /app/data/test.txt
The file can then be checked with:
ls /app/data
📈 Scaling
Kubernetes allows the application to run multiple Pods.
Scale the application:
kubectl scale deployment node-app --replicas=4
Check the deployment:
kubectl get deployment
Check the Pods:
kubectl get pods
Kubernetes creates or removes Pods to match the desired replica count.
🔄 Rolling Updates
When the application image or Deployment configuration changes, Kubernetes can perform a rolling update.
Apply the updated configuration:
kubectl apply -f k8s/deployment.yaml
Check the rollout:
kubectl rollout status deployment/node-app
View ReplicaSets:
kubectl get replicasets
Rollback if required:
kubectl rollout undo deployment/node-app
❤️ Kubernetes Self-Healing
One of the important Kubernetes features demonstrated in this project is self-healing.
If a Pod managed by the Deployment fails or is deleted:
kubectl delete pod <pod-name>
Kubernetes automatically creates a replacement Pod to maintain the desired replica count.
Check:
kubectl get pods
This happens because the Deployment continuously works to maintain the desired state.
🔍 Useful Kubernetes Commands
Check all resources
kubectl get all
Check Pods
kubectl get pods
Check Deployments
kubectl get deployments
Check ReplicaSets
kubectl get replicasets
Check ConfigMaps
kubectl get configmaps
Check Secrets
kubectl get secrets
Check Persistent Volumes
kubectl get pv
Check Persistent Volume Claims
kubectl get pvc
Describe a Pod
kubectl describe pod <pod-name>
View Pod logs
kubectl logs <pod-name>
Execute a command inside a Pod
kubectl exec -it <pod-name> -- ls
🚀 Deployment Steps
1. Start Kubernetes
Make sure your Kubernetes cluster is running.
Verify:
kubectl get nodes
2. Build the Docker Image
From the project directory:
docker build -t kubernetes-node-app:2.0 ./app
3. Apply Kubernetes Resources
Apply the ConfigMap:
kubectl apply -f k8s/configmap.yaml
Apply the Secret:
kubectl apply -f k8s/secret.yaml
Apply the PersistentVolume:
kubectl apply -f k8s/pv.yaml
Apply the PersistentVolumeClaim:
kubectl apply -f k8s/pvc.yaml
Apply the Deployment:
kubectl apply -f k8s/deployment.yaml
4. Verify Deployment
kubectl get pods
kubectl get deployment
kubectl get pv
kubectl get pvc
🔐 GitHub
The project is maintained using Git and GitHub.
Initialize Git:
git init
Add files:
git add .
Commit:
git commit -m "Initial Kubernetes project"
Connect the GitHub repository:
git remote add origin <your-github-repository-url>
Push the project:
git branch -M main
git push -u origin main
📌 Key Kubernetes Concepts Learned
Through this project, the following Kubernetes concepts were implemented:
Concept
Purpose
Pod
Runs the application container
Deployment
Manages application Pods
ReplicaSet
Maintains the desired number of Pods
ConfigMap
Stores non-sensitive configuration
Secret
Stores sensitive configuration
PersistentVolume
Provides persistent storage
PersistentVolumeClaim
Requests storage
Scaling
Increases/decreases application replicas
Rolling Update
Updates application without stopping all Pods
Self-Healing
Recreates failed Pods automatically
kubectl
Command-line tool for Kubernetes
🎯 Project Outcome
This project demonstrates how a Node.js application can be deployed and managed using Kubernetes while using configuration management, secrets, persistent storage, scaling, rolling updates, and self-healing.
It provides practical experience with the core Kubernetes concepts used in modern DevOps and cloud-native environments.

### One small recommendation

For your GitHub repository, **keep `.gitignore`**. Don't delete it. It helps prevent files such as `.env`, secrets, logs, and Terraform state from accidentally being pushed to GitHub.

Your GitHub structure should ideally look like:

```text
kubernetes-project
│
├── app
├── k8s
├── .gitignore
└── README.md
The -- file shown in your screenshot is the unwanted file; .gitignore is useful and should stay.