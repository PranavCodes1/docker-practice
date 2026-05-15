# Helm Package Manager for Kubernetes

## Introduction

Helm is a package manager for Kubernetes. It simplifies Kubernetes application deployment by packaging multiple Kubernetes YAML manifests into reusable Helm Charts.

Instead of manually creating deployments, services, configmaps, secrets and other Kubernetes resources, Helm allows deploying complex applications using a single command.

In this task, Helm was used to deploy the Kube Prometheus Stack for monitoring a Kubernetes cluster.

---

# Objectives

The main objectives of this task were:

* Understand what Helm is
* Learn why Helm is used in Kubernetes
* Learn Helm Charts and repositories
* Understand Helm releases
* Understand values.yaml
* Deploy Kube Prometheus Stack using Helm
* Understand Prometheus and Grafana basics
* Explore monitoring dashboards in Grafana

---

# What is Helm?

Helm is a package manager for Kubernetes.

Similar to:

* apt for Ubuntu
* yum for RHEL
* brew for macOS
* npm for Node.js

Helm is used to install and manage Kubernetes applications.

---

# Why Helm is Used

Without Helm:

* Multiple YAML files must be created manually
* Complex applications take time to deploy
* Configuration management becomes difficult
* Upgrades and rollback are harder

With Helm:

* Applications can be deployed using a single command
* Configurations can be customized using values.yaml
* Applications can be upgraded easily
* Rollbacks are supported
* Reusable charts simplify deployments

---

# Helm Concepts

## 1. Helm Charts

A Helm Chart is a packaged collection of Kubernetes YAML files and templates.

Charts are stored in repositories and can be installed directly.

---

## 2. Helm Repositories

Repositories store Helm Charts.

Public Helm charts are available on Artifact Hub.

Example repository:

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```

---

## 3. Helm Releases

A Helm Release is a deployed instance of a Helm Chart.

Multiple releases of the same chart can exist:

* dev
* test
* prod

---

## 4. values.yaml

values.yaml contains configuration values for a Helm Chart.

It allows customizing deployments without manually editing Kubernetes YAML manifests.

---

# What is Prometheus?

Prometheus is a monitoring and metrics collection tool.

It collects metrics from Kubernetes components such as:

* CPU usage
* Memory usage
* Pod metrics
* Node metrics
* Network metrics

Prometheus stores time-series data and is widely used for Kubernetes monitoring.

---

# What is Grafana?

Grafana is a visualization and dashboard platform.

Grafana uses data collected by Prometheus and displays it through dashboards and graphs.

It helps monitor:

* Cluster health
* Resource usage
* Pod performance
* Node metrics
* Kubernetes workloads

---

# Helm Installation

## Check Helm Version

```bash
helm version
```

## Install Helm

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

---

# Kubernetes Verification

```bash
kubectl get nodes
```

---

# Adding Helm Repository

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update
```

---

# Creating Namespace

```bash
kubectl create namespace monitoring
```

---

# Deploying Kube Prometheus Stack

```bash
helm install monitoring prometheus-community/kube-prometheus-stack \
--namespace monitoring
```

This command automatically installed:

* Prometheus
* Grafana
* Alertmanager
* kube-state-metrics
* node-exporter
* prometheus-operator

---

# Verifying Pods

```bash
kubectl get pods -n monitoring
```

Multiple monitoring pods were successfully created and running.

---

# Checking Helm Releases

```bash
helm list -n monitoring
```

---

# Checking Helm Release Status

```bash
helm status monitoring -n monitoring
```

---

# Generating values.yaml

```bash
helm show values prometheus-community/kube-prometheus-stack > values.yaml
```

The generated values.yaml file contains configurable deployment settings for the chart.

---

# Accessing Grafana Dashboard

## Port Forwarding

```bash
kubectl port-forward svc/monitoring-grafana 3000:80 -n monitoring
```

## Grafana Login

Username:

```text
admin
```

Get Password:

```bash
kubectl get secret monitoring-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 --decode
```

---

# Grafana Dashboards Explored

The following dashboards were explored:

* Grafana Overview
* Kubernetes / Compute Resources / Cluster
* Kubernetes / Compute Resources / Pod

These dashboards displayed:

* CPU usage
* Memory usage
* Pod metrics
* Cluster monitoring data

---

# Helm Commands Used

```bash
helm version
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install monitoring prometheus-community/kube-prometheus-stack --namespace monitoring
helm list -n monitoring
helm status monitoring -n monitoring
helm show values prometheus-community/kube-prometheus-stack > values.yaml
helm search repo prometheus
```

---

# Learnings

* Learned how Helm simplifies Kubernetes deployments
* Understood Helm Charts, Repositories and Releases
* Learned the purpose of values.yaml
* Understood Kubernetes monitoring basics
* Learned Prometheus and Grafana basics
* Understood how monitoring stacks are deployed using Helm
* Explored Grafana dashboards and monitoring metrics
* Learned how Helm manages complex Kubernetes applications

---

---

# Conclusion

Helm greatly simplifies Kubernetes application deployment and management.

Using Helm, the Kube Prometheus Stack was successfully deployed with a single command, demonstrating how complex monitoring systems can be managed efficiently in Kubernetes environments.

This task helped in understanding:

* Kubernetes monitoring
* Prometheus and Grafana basics
* Helm deployment workflows
* Helm repositories and releases
* Kubernetes observability concepts
