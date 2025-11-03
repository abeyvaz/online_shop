Excellent 😎 — here’s a **fully polished, professional GitHub README.md** version of your Online Shop project, complete with emojis, badges, proper formatting, and corrected YAML.
It’s clean, readable, and perfect for showcasing DevOps/Docker/Kubernetes workflow skills on GitHub.

---

# 🛍️ Online Shop — Docker & Kubernetes Deployment Guide

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge\&logo=docker\&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge\&logo=kubernetes\&logoColor=white)
![DevOps](https://img.shields.io/badge/DevOps-A42E2B?style=for-the-badge\&logo=azuredevops\&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

---

## 🧠 Overview

This project demonstrates how to containerize and deploy the **Online Shop** web application using **Docker** and **Kubernetes** (Kind or Minikube).
It walks through every step — from building and pushing Docker images to deploying and exposing your app inside a Kubernetes cluster.

---

## 🧩 Step 1. Clone the Repository

```bash
git clone <repository-url>
cd online_shop
```

---

## 🐳 Step 2. Build the Docker Image

```bash
docker build -t online_shop:latest .
```

---

## ▶️ Step 3. Run the Docker Container Locally

```bash
docker run -d -p 5173:5173 online_shop:latest
```

Verify if the container is running:

```bash
docker ps
```

Then open **[http://localhost:5173](http://localhost:5173)** in your browser 🚀

---

## 📤 Step 4. Push the Image to Docker Hub

Tag and push the image:

```bash
docker tag online_shop:latest jrvaz1/online-shop:latest
docker push jrvaz1/online-shop:latest
```

---

## ☸️ Step 5. Deploy to Kubernetes

Create a separate directory for your Kubernetes manifests:

```bash
mkdir K8s && cd K8s
```

---

### 🧾 Namespace (`namespace.yml`)

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: online-shop
```

**Apply:**

```bash
kubectl apply -f namespace.yml
kubectl get ns
```

---

### 📦 Deployment (`deployment.yml`)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: online-shop-deployment
  namespace: online-shop
  labels:
    app: online-shop
spec:
  replicas: 2
  selector:
    matchLabels:
      app: online-shop
  template:
    metadata:
      labels:
        app: online-shop
    spec:
      containers:
      - name: online-shop-container
        image: jrvaz1/online-shop:latest
        ports:
        - containerPort: 5173
```

**Apply and verify pods:**

```bash
kubectl apply -f deployment.yml
kubectl get pods -n online-shop
```

---

### 🌐 Service (`service.yml`)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: online-shop-svc
  namespace: online-shop
spec:
  selector:
    app: online-shop
  ports:
    - protocol: TCP
      port: 5173
      targetPort: 5173
  type: ClusterIP
```

**Apply and verify:**

```bash
kubectl apply -f service.yml
kubectl get all -n online-shop
```

---

## 🚀 Step 6. Access the Application

Forward the service port to your local machine:

```bash
kubectl port-forward svc/online-shop-svc -n online-shop 5173:5173 --address=0.0.0.0
```

Now open your browser and visit 👉 [http://localhost:5173](http://localhost:5173)

---

## 🧹 Cleanup Resources

```bash
kubectl delete namespace online-shop
docker system prune -af
```

---

## 💡 Tech Stack

| Tool                                | Purpose                                 |
| ----------------------------------- | --------------------------------------- |
| 🐳 **Docker**                       | Containerization of the Online Shop app |
| ☸️ **Kubernetes (Kind / Minikube)** | Orchestrating containers                |
| 🧾 **YAML**                         | Kubernetes resource definitions         |
| 📦 **Docker Hub**                   | Hosting container images                |

---

## 🧑‍💻 Author

**Abey Vaz**
🔗 [Docker Hub](https://hub.docker.com/u/jrvaz1)
💼 *DevOps Enthusiast | Infrastructure Specialist | Cloud Learner*

---

Would you like me to add a **small architecture diagram** (app → service → deployment → namespace) in Markdown or image format for visual clarity in your README?








    



    

    

