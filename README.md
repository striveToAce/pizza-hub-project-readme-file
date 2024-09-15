
# Pizza Fusion - Running and Testing the Application

This guide provides instructions for running and testing the **Pizza Fusion** application and ensuring all microservices work together seamlessly.

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Docker Hub Images](#docker-hub-images)
3. [Running Microservices Locally with Docker](#running-microservices-locally-with-docker)
4. [Kubernetes Deployment](#kubernetes-deployment)
5. [Kubernetes Verification and Port Forwarding](#kubernetes-verification-and-port-forwarding)
6. [Testing the Application](#testing-the-application)
7. [Key Kubernetes Commands](#key-kubernetes-commands)
8. [Troubleshooting](#troubleshooting)

---

## 1. Prerequisites
- **Docker**: Ensure Docker is installed and running on your system.
- **Kubernetes**: You should have `kubectl` set up to interact with your Kubernetes cluster.
- **Node.js**: Used for local testing if needed.

---

## 2. Docker Hub Images

The microservices have already been pushed to **Docker Hub**:

- pizza-fusion-order-msc: `docker.io/docker380431/pizza-fusion-order-msc`
- pizza-fusion-menu-msc: `docker.io/docker380431/pizza-fusion-menu-msc`
- pizza-fusion-chef-msc: `docker.io/docker380431/pizza-fusion-chef-msc`
- pizza-fusion-frontend: `docker.io/docker380431/pizza-fusion-frontend`

These images are available for deployment.

---

## 3. Running Microservices Locally with Docker

To run the microservices locally using Docker, follow these steps:

### Pull the Docker Images:
```bash
docker pull docker.io/docker380431/pizza-fusion-order-msc
docker pull docker.io/docker380431/pizza-fusion-menu-msc
docker pull docker.io/docker380431/pizza-fusion-chef-msc
docker pull docker.io/docker380431/pizza-fusion-frontend
```

### Run Each Microservice in Docker:

For **Order Service**:
```bash
docker run -d -p 3001:3001 --name pizza-fusion-order-msc docker.io/docker380431/pizza-fusion-order-msc
```

For **Menu Service**:
```bash
docker run -d -p 3002:3002 --name pizza-fusion-menu-msc docker.io/docker380431/pizza-fusion-menu-msc
```

For **Chef Service**:
```bash
docker run -d -p 3003:3003 --name pizza-fusion-chef-msc docker.io/docker380431/pizza-fusion-chef-msc
```

For **Frontend**:
```bash
docker run -d -p 3000:3000 --name pizza-fusion-frontend docker.io/docker380431/pizza-fusion-frontend
```

### Verify Running Containers:
```bash
docker ps
```
Ensure all services are running on ports 3000 (frontend), 3001 (order service), 3002 (menu service), and 3003 (chef service).

---

## 4. Kubernetes Deployment

To deploy everything to Kubernetes, follow these steps:

### Deploy the Order Service:
```bash
kubectl apply -f k8s/order/deployment.yml
kubectl apply -f k8s/order/service.yml
```

### Deploy the Menu Service:
```bash
kubectl apply -f k8s/menu/deployment.yml
kubectl apply -f k8s/menu/service.yml
```

### Deploy the Chef Service:
```bash
kubectl apply -f k8s/chef/deployment.yml
kubectl apply -f k8s/chef/service.yml
```

### Deploy the Frontend:
```bash
kubectl apply -f k8s/frontend/deployment.yml
kubectl apply -f k8s/frontend/service.yml
```

---

## 5. Kubernetes Verification and Port Forwarding

### Verify Pods and Services:
Check that all pods and services are running:
```bash
kubectl get pods
kubectl get services
```

### Port Forwarding for Local Testing:
If you want to access the services locally, you can forward ports from the Kubernetes cluster to your local machine:

For **Frontend** (port 3000):
```bash
kubectl port-forward service/pizza-fusion-frontend-service 3000:3000
```

For **Order Service** (port 3001):
```bash
kubectl port-forward service/pizza-fusion-order-service 3001:3001
```

For **Menu Service** (port 3002):
```bash
kubectl port-forward service/pizza-fusion-menu-service 3002:3002
```

For **Chef Service** (port 3003):
```bash
kubectl port-forward service/pizza-fusion-chef-service 3003:3003
```

---

## 6. Testing the Application

- **Customer View**: Select items, view cart, and place orders.
- **Admin View**: Manage menu items and monitor real-time order updates.
- **Real-Time Updates**: Ensure the Supabase subscription for order updates is working in real time.

---

## 7. Key Kubernetes Commands

- **Apply Kubernetes manifests**:
```bash
kubectl apply -f <filename>.yml
```

- **Delete deployments and services**:
```bash
kubectl delete -f <filename>.yml
```

- **Check pods and services**:
```bash
kubectl get pods
kubectl get services
```

- **Port forwarding for local testing**:
```bash
kubectl port-forward service/<service-name> <local-port>:<container-port>
```

---

## 8. Troubleshooting

- **Check logs of a Kubernetes pod**:
```bash
kubectl logs <pod-name>
```

- **Describe a service or deployment** (to check for issues):
```bash
kubectl describe service <service-name>
kubectl describe deployment <deployment-name>
```

---

This guide should help you run, test, and deploy the **Pizza Fusion** application using Docker and Kubernetes. Let me know if you need further clarifications or assistance!
