# 🚀 Blue-Green Deployment Skill Test

## 📌 Project Overview

This project demonstrates end-to-end deployment of a containerized full-stack application using:

- Node.js + Express (Backend)
- MongoDB (Database)
- Two React/Vite Frontends (Blue & Green)
- Docker & Docker Compose
- Kubernetes (Minikube)
- Blue-Green Deployment Strategy

The goal is to implement zero-downtime deployment using Kubernetes service switching between blue and green environments.

---

## 🏗️ Architecture

Blue-Green deployment ensures zero downtime by running two identical environments:

- **Blue Environment** → Current Production
- **Green Environment** → New Version

Traffic is switched using a Kubernetes Service selector.

---

## ⚙️ Prerequisites

Ensure the following tools are installed:

- Git
- Node.js (v18+)
- Docker & Docker Compose
- kubectl
- Minikube

---

## 🔹 Part 1: Local Deployment

### Step 1: Clone Repository
```bash
git clone https://github.com/Sirajmd1/HeroVired_Skilltest2.git
cd HeroVired_Skilltest2
```

### Step 2: Run MongoDB
```bash
docker run -d -p 27017:27017 --name mongodb mongo
```

### Step 3: Start Backend
```bash
cd backend
npm install
npm start
```

Create `.env` file:
```env
PORT=5000
MONGO_URI=mongodb://localhost:27017/bgapp
```

### Step 4: Start Frontend Blue
```bash
cd ../frontend-blue
npm install
npm start
```

### Step 5: Start Frontend Green
```bash
cd ../frontend-green
npm install
npm start
```

---

## ✅ Validation

- Backend: http://localhost:5000
- Blue UI: http://localhost:3100
- Green UI: http://localhost:3200

---

## 🐳 Part 2: Docker Containerization

### Build & Run
```bash
docker compose up --build -d
```

### Verify
```bash
docker ps
```

---

## ☸️ Part 3: Kubernetes Deployment

### Start Minikube
```bash
minikube start --driver=docker
```

### Enable Addons
```bash
minikube addons enable ingress
minikube addons enable metrics-server
```

### Use Minikube Docker
```bash
eval $(minikube docker-env)
```

### Build Images
```bash
docker build -t backend:v1 ./backend
docker build -t frontend-blue:v1 ./frontend-blue
docker build -t frontend-green:v1 ./frontend-green
```

### Deploy to Kubernetes
```bash
kubectl apply -f k8s/
```

### Verify
```bash
kubectl get pods
kubectl get services
kubectl get deployments
```

### Access App
```bash
minikube service frontend-service --url
```

---

## 🔵🟢 Part 4: Blue-Green Deployment

### Switch to Green
```bash
kubectl patch service frontend-service \
  -p '{"spec":{"selector":{"app":"frontend","version":"green"}}}'
```

### Rollback to Blue
```bash
kubectl patch service frontend-service \
  -p '{"spec":{"selector":{"app":"frontend","version":"blue"}}}'
```

---

## ✅ Results

- Zero downtime deployment achieved
- Instant rollback capability
- Kubernetes service-based traffic routing

---

## ⚠️ Challenges Faced

### 1. Disk Space Issues
Resolved using:
```bash
docker system prune -a
```

### 2. GitHub Authentication Error
Solution: Used Personal Access Token / SSH

### 3. Kubernetes Image Pull Issue
```yaml
imagePullPolicy: Never
```

---

## 📸 Screenshots Required

- Local deployment
- Docker containers running
- Kubernetes pods/services
- Blue → Green switch

---

## 🎯 Learning Outcomes

- Docker Containerization
- Kubernetes Deployment
- Service Discovery
- Blue-Green Deployment
- Zero Downtime Release Strategy

---

## 👤 Author

**Sirajuddin Mohammed**

---

