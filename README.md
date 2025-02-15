# 🚀 Chat App Deployment Using Kubernetes 🛠️

## 📌 Overview
This project aims to provide a deployed 3-tier chat application using Kubernetes. The application consists of a frontend, backend, and a MongoDB database, all orchestrated within a Kubernetes Minikube cluster.

## ✅ Prerequisites
- ⚡ Kubernetes Minikube cluster set up and configured
- 🖥️ kubectl installed and configured to interact with the cluster
- 🐳 Docker and Docker Hub installed
- 🌐 Ingress controller installed (e.g., Nginx Ingress Controller)
  
## 🏗️ Build and Run the Application:
Follow these steps to build and run the application:

### 1️⃣ Navigate to the Kubernetes Configurations Directory 📂
```sh
cd k8s
```
Ensure you are in the `k8s` directory where all the Kubernetes manifest files are located.

### 2️⃣ Apply Namespace Configuration 🏷️
```sh
kubectl apply -f namespace.yml
```
🔹 Creates a namespace `chat-app` to logically separate application resources within the cluster.

### 3️⃣ Deploy Persistent Volume (PV) for MongoDB 💾
```sh
kubectl apply -f mongodb-pv.yml -n chat-app
```
🔹 Defines storage for MongoDB to persist data even if the pod restarts. Ensures data remains intact after rescheduling or node failure.

### 4️⃣ Deploy Persistent Volume Claim (PVC) for MongoDB 📦
```sh
kubectl apply -f mongodb-pvc.yml -n chat-app
```
🔹 Requests storage from the Persistent Volume (PV) for MongoDB, ensuring it gets the required storage capacity.

### 5️⃣ Apply All Kubernetes Manifests 📜
```sh
kubectl apply -f . -n chat-app
```
🔹 Deploys all resources inside the `k8s` directory to the `chat-app` namespace, including frontend, backend, MongoDB deployment, services, and ingress configuration.

### 6️⃣ Forward Ingress Nginx Controller Port (Optional for Local Testing) 🌍
```sh
sudo -E kubectl port-forward service/ingress-nginx-controller 80:80 -n ingress-nginx
```
🔹 Forwards port 80 of the `ingress-nginx` service to localhost. Allows access to the application without an external load balancer.

### 7️⃣ Access the Application 🌐
After port forwarding:
- 🔗 Open a browser and visit `http://localhost`. You should see the Nginx default page, confirming ingress is working.
- 🔗 Navigate to `http://chat-app.com` for the frontend.
- 🔗 Navigate to `http://chat-app.com/api` for the backend.

