# Kubernetes Setup with Minikube & kubectl

This guide provides a step-by-step process to install **kubectl** and **minikube**, create a **multi-node Kubernetes cluster**, and enable the **Dashboard** for cluster management.

---

## 📌 Prerequisites
- Linux workstation (x86_64 / amd64 shown here).
- A container runtime or hypervisor (Docker recommended).
- `sudo` access.

---

## ⚙️ 1. Install `kubectl`


# Download the latest stable kubectl for Linux amd64
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
# Make it executable
chmod +x kubectl

# Install to /usr/local/bin
```
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
# Verify
```
kubectl version --client
```
## ⚙️ 2. Install minikube
# Download minikube binary
```
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
```
# Install
```
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
# Verify
```
minikube version
```
## 3. Start a Multi-Node Cluster (jayveer with 2 nodes)
```
minikube start -p jayveer --nodes=2 --driver=docker --cpus=4 --memory=8192
```
## Cluster Setup Instructions

- Create a profile named **jayveer**.  
- Configure the cluster with **2 nodes**:  
  - **1 Control-Plane Node**  
  - **1 Worker Node**  
- Adjust `--cpus` and `--memory` according to your system resources.

## 4. Verify Cluster & Nodes

# Check current context
```
kubectl config current-context
```
# List nodes
```
kubectl get nodes -o wide
```
# Minikube status
```
minikube status -p jayveer
```
## 5. Manage Minikube Profiles
# List profiles
```
minikube profile list
```
# Stop cluster
```
minikube stop -p jayveer
```
# Start cluster again
```
minikube start -p jayveer --nodes=2
```
# Delete cluster
```
minikube delete -p jayveer
```
## 6. Enable & Access Kubernetes Dashboard
# Enable dashboard addon
```
minikube addons enable dashboard -p jayveer
```
# Open dashboard in browser
```
minikube dashboard -p jayveer
```
# Or get dashboard URL
```
minikube dashboard -p jayveer --url
```
## 7. Useful Extra Commands
# Troubleshooting logs
```
minikube logs -p jayveer
```
# List nodes created
```
minikube node list -p jayveer
```
# Add or remove nodes
```
minikube node add -p jayveer
minikube node delete -p jayveer <node-name>
```
# List enabled addons
```
minikube addons list -p jayveer
```
## 8. Troubleshooting

- If `minikube start` fails → check the driver:  
  - `--driver=docker`  
  - `--driver=virtualbox`  
  - (use the one supported by your system)

- For **persistent volumes in multi-node setups** → enable the **CSI hostpath addon**.


