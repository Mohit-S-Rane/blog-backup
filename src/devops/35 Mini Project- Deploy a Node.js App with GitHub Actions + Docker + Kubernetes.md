# Mini Project: Deploy a Node.js App with GitHub Actions + Docker + Kubernetes 🚀

**Looking to level up your DevOps skills?** This hands-on project walks you through deploying a simple Node.js app using **GitHub Actions** (for CI/CD), **Docker** (for containerization), and **Kubernetes** (for orchestration). It’s the perfect way to put theory into practice, whether you’re a student exploring DevOps or a developer seeking real-world experience.

---

## 🌟 Introduction: Why This Matters

Modern software deployment is all about **automation and scalability**. By combining GitHub Actions, Docker, and Kubernetes, you get a **real-world glimpse into how modern tech teams ship code reliably and efficiently**.

This mini project teaches you:

✅ How to containerize an app with Docker.

✅ How to set up CI/CD using GitHub Actions.

✅ How to deploy to Kubernetes.

---

## 1️⃣ Prerequisites

Before we jump in, make sure you have:

🔹 **Basic Node.js knowledge** (e.g., `express` server).

🔹 **Docker** installed locally.

🔹 **kubectl** and **minikube** (or Docker Desktop with Kubernetes enabled) for local clusters.

🔹 A **GitHub account** (free).

💡 **Tip**: If you’re new to Docker or Kubernetes, start with a refresher on these basics.

---

## 2️⃣ Step 1: Create a Simple Node.js App

🔹 **Setup**

- Initialize a new Node.js app:
    
    ```bash
    mkdir node-k8s-demo && cd node-k8s-demo
    npm init -y
    npm install express
    
    ```
    
- Create a simple server (`index.js`):
    
    ```jsx
    const express = require('express');
    const app = express();
    const PORT = process.env.PORT || 3000;
    
    app.get('/', (req, res) => {
      res.send('Hello, Kubernetes!');
    });
    
    app.listen(PORT, () => {
      console.log(`Server running on port ${PORT}`);
    });
    
    ```
    

---

## 3️⃣ Step 2: Dockerize the App

🔹 **Create a `Dockerfile`:**

```
# Use Node.js official image
FROM node:18-alpine

# Set working directory
WORKDIR /usr/src/app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the code
COPY . .

# Expose port
EXPOSE 3000

# Command to run the app
CMD ["node", "index.js"]

```

🔹 **Build and test locally:**

```bash
docker build -t node-k8s-demo .
docker run -p 3000:3000 node-k8s-demo

```

---

## 4️⃣ Step 3: Push to GitHub

🔹 **Initialize Git and push your code:**

```bash
git init
git remote add origin <your-repo-url>
git add .
git commit -m "Initial commit"
git push -u origin main

```

---

## 5️⃣ Step 4: Set Up GitHub Actions

🔹 **Create `.github/workflows/deploy.yml`:**

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ "main" ]

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Login to DockerHub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build and push image
        uses: docker/build-push-action@v5
        with:
          push: true
          tags: ${{ secrets.DOCKER_USERNAME }}/node-k8s-demo:latest

```

🔹 **Add DockerHub credentials** in your repo’s **Secrets**.

💡 **Pro Tip**: Use GitHub’s UI to add secrets: `Settings -> Secrets -> Actions`.

---

## 6️⃣ Step 5: Kubernetes Deployment

🔹 **Write a `deployment.yaml`:**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: node-k8s-demo
spec:
  replicas: 2
  selector:
    matchLabels:
      app: node-k8s-demo
  template:
    metadata:
      labels:
        app: node-k8s-demo
    spec:
      containers:
        - name: node-k8s-demo
          image: <dockerhub-username>/node-k8s-demo:latest
          ports:
            - containerPort: 3000

```

🔹 **Write a `service.yaml`:**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: node-k8s-demo-service
spec:
  type: NodePort
  selector:
    app: node-k8s-demo
  ports:
    - protocol: TCP
      port: 3000
      targetPort: 3000
      nodePort: 30001

```

🔹 **Deploy it locally:**

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl get pods
minikube service node-k8s-demo-service

```

---

## 7️⃣ Step 6: Recap & What’s Next

✅ **What you’ve built**:

- A Node.js app that runs in a Docker container.
- A CI/CD pipeline that builds and pushes the image to DockerHub.
- A Kubernetes deployment that runs the app with multiple replicas.

✅ **What you’ve learned**:

- How GitHub Actions automate your build process.
- How Docker helps create portable app containers.
- How Kubernetes orchestrates containers at scale.

---

## Conclusion

This mini project is a **stepping stone** to mastering real-world DevOps.

✅ **For College Students**: A perfect portfolio piece to showcase during interviews.

✅ **For Corporate Developers**: A hands-on way to understand modern deployment workflows.

✅ **For Leaders**: A model for how CI/CD, Docker, and Kubernetes can integrate seamlessly.

📌 **Next Steps**:

- Try adding a Helm chart to manage your deployment.
- Explore GitOps tools like ArgoCD to automate Kubernetes rollouts.
- Set up monitoring with Prometheus and Grafana.

With this project, you’re one step closer to DevOps mastery. Ready to take on the cloud? 🚀🔧