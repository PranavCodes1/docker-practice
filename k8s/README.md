# Kubernetes Deployment - Docker Practice

## Overview

This project demonstrates deploying a Dockerized Python application on Kubernetes using Kind (Kubernetes in Docker) inside GitHub Codespaces.

The goal of this task was to understand Kubernetes basics and deploy an application using Kubernetes resources such as Deployments and Services.

---

# Technologies Used

* Docker
* Kubernetes
* Kind (Kubernetes in Docker)
* kubectl
* GitHub Codespaces
* Python

---

# Kubernetes Concepts Learned

* Kubernetes Architecture
* Master Node & Worker Nodes
* Pods
* Deployments
* Services
* Namespaces
* YAML Configuration Files
* kubectl Commands
* Port Forwarding
* Kubernetes Networking Basics

---

# Kubernetes Cluster Setup

Since Docker support on local macOS older version was unstable, the Kubernetes setup was completed using GitHub Codespaces.

## Steps Followed

### 1. Verified Docker

```bash
docker ps
```

### 2. Installed Kind

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

### 3. Created Kubernetes Cluster

```bash
kind create cluster
```

### 4. Verified Cluster

```bash
kubectl get nodes
kubectl get pods -A
kubectl cluster-info
```

---

# Application Deployment

## Deployment YAML

Created:

```text
k8s/deployment.yaml
```

Deployment responsibilities:

* Creates Pods
* Maintains desired replicas
* Restarts failed Pods automatically

Application image used:

```text
pranavcodes1/sample-app
```

---

# Service Configuration

Created:

```text
k8s/service.yaml
```

Service Type Used:

```text
NodePort
```

Responsibilities:

* Exposes application
* Routes traffic to Pods
* Provides stable networking

---

# Verification Commands Used

## Check Pods

```bash
kubectl get pods
```

## Check Deployments

```bash
kubectl get deployments
```

## Check Services

```bash
kubectl get svc
```

## View Logs

```bash
kubectl logs <pod-name>
```

## Describe Resources

```bash
kubectl describe pod <pod-name>
kubectl describe deployment sample-app-deployment
```

---

# Port Forwarding

Used port forwarding to access the application:

```bash
kubectl port-forward service/sample-app-service 5000:5000
```

---

# Issues Faced

## Issue

Docker support on local macOS Catalina system was unstable.

## Resolution

Used GitHub Codespaces with Kind for Kubernetes setup and deployment.

---

# Project Structure

```text
project/
├── app/
├── Dockerfile
├── docker-compose.yml
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
└── README.md
```

---

# Outcome

Successfully:

* Created Kubernetes cluster
* Deployed Dockerized application
* Created Deployments and Services
* Exposed application using Kubernetes Service
* Verified Pods, Deployments, Services, and Logs using kubectl
* Understood Kubernetes deployment workflow
