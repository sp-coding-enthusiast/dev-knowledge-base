# kind (Kubernetes in Docker) – Quick Start Guide

This document is a clean, beginner‑friendly Markdown guide for setting up **kind** and using basic **kubectl** commands.

---

## 📚 References

* kind Docs: [https://kind.sigs.k8s.io/docs/user/quick-start/](https://kind.sigs.k8s.io/docs/user/quick-start/)
* Sample kind Config: [https://raw.githubusercontent.com/kubernetes-sigs/kind/main/site/content/docs/user/kind-example-config.yaml](https://raw.githubusercontent.com/kubernetes-sigs/kind/main/site/content/docs/user/kind-example-config.yaml)
* Kubernetes Docs: [https://kubernetes.io/docs/home/](https://kubernetes.io/docs/home/)
* kubectl Quick Reference: [https://kubernetes.io/docs/reference/kubectl/quick-reference/](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

---

## 🧰 Prerequisites

* Docker installed and running
* kubectl installed
* Homebrew (macOS) or equivalent package manager

---

## 🚀 Installing kind

```bash
brew install kind
```

Verify installation:

```bash
kind version
```

---

## 🏗️ Creating Clusters

### 1️⃣ Create a Single‑Node Cluster

```bash
kind create cluster --name my-first-kind
```

Verify cluster info:

```bash
kubectl cluster-info --context kind-my-first-kind
```

---

### 2️⃣ Create a Multi‑Node Cluster (1 Control Plane + 2 Workers)

Create a file named `config.yaml`:

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

Create the cluster:

```bash
kind create cluster --name my-first-kind --config config.yaml
```

---

## 🧹 Deleting a Cluster

```bash
kind delete cluster --name my-first-kind
```

---

## 📋 Listing Clusters

```bash
kind get clusters
```

---

## 🔁 Switching Kubernetes Context

```bash
kubectl config use-context kind-my-first-kind
```

Check current context:

```bash
kubectl config current-context
```

---

# ☸️ Kubernetes Resources & kubectl Commands

---

## 📦 Pod Creation

```bash
kubectl run nginx --image=nginx
```

Creates a pod named **nginx** using the **nginx** image.

---

## 🚢 Deployment & Service

### Create Deployment

```bash
kubectl create deploy nginx-deploy --image=nginx
```

### Expose Deployment as a Service

```bash
kubectl expose deploy nginx-deploy --port=80
```

---

## 🔍 Describing Resources

```bash
kubectl describe pod nginx
```

Generic format:

```bash
kubectl describe <resource-type> <resource-name>
```

---

## 📜 Viewing Logs

```bash
kubectl logs nginx
```

---

## 📊 Getting Resources

```bash
kubectl get pods
kubectl get deploy
kubectl get svc
kubectl get ep
```

---

## ✏️ Editing Resources

```bash
kubectl edit deploy nginx-deploy
```

---

## 🔄 Rollout Management

Check rollout status:

```bash
kubectl rollout status deploy/nginx-deploy
```

Restart deployment:

```bash
kubectl rollout restart deploy/nginx-deploy
```

Undo last rollout:

```bash
kubectl rollout undo deploy/nginx-deploy
```

---

## 📄 Applying Configuration Files

Create resources:

```bash
kubectl create -f filename.yaml
```

Apply (create or update) resources:

```bash
kubectl apply -f filename.yaml
```

---

## ✅ Next Steps

* Deploy a sample app and expose it via NodePort
* Learn about Pods vs Nodes vs Services
* Practice with `kubectl explain` and YAML manifests
* Explore Ingress, ConfigMaps, and Secrets

---

Happy Kubernetes learning 🚀
