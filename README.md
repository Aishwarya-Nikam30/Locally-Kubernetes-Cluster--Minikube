
# 🚀 Build a Kubernetes Cluster Locally with Minikube

## 📌 Objective
Deploy and manage applications in a local Kubernetes cluster using **Minikube** on Windows with PowerShell.

## 🛠 Tools Used
- [Minikube](https://minikube.sigs.k8s.io/docs/) - Local Kubernetes cluster
- [kubectl](https://kubernetes.io/docs/tasks/tools/) - Kubernetes command-line tool
- [Docker](https://www.docker.com/) - Minikube driver for container runtime
- PowerShell (Windows)

## ⚙ Detailed Steps

### 1️⃣ Install Minikube
Download the Minikube executable:
```powershell
Invoke-WebRequest -OutFile minikube.exe https://storage.googleapis.com/minikube/releases/latest/minikube-windows-amd64.exe
```
👉 **Why:** Minikube is used to create a local Kubernetes cluster for testing and learning.

Move `minikube.exe` to a directory like `C:\minikube\` and add this directory to your system `Path` so it can be called from anywhere.

### 2️⃣ Install kubectl
Download `kubectl`:
```powershell
Invoke-WebRequest -OutFile kubectl.exe https://dl.k8s.io/release/v1.29.0/bin/windows/amd64/kubectl.exe
```
👉 **Why:** `kubectl` is the CLI tool for interacting with the Kubernetes API server to manage the cluster.

Move `kubectl.exe` to `C:\kubectl\` and update the system `Path` similarly.

### 3️⃣ Verify Installation
```powershell
minikube version
kubectl version --client
```
👉 **Why:** Ensures both tools are installed and accessible.

### 4️⃣ Start Minikube Cluster
```powershell
minikube start --driver=docker
```
👉 **Why:** This starts a single-node Kubernetes cluster locally using Docker.

Verify node:
```powershell
kubectl get nodes
```

### 5️⃣ Create Deployment
Create a file `deployment.yaml`:
```
Apply:
```powershell
kubectl apply -f .\deployment.yaml
kubectl get pods
```
👉 **Why:** The deployment manages multiple replicas of NGINX pods.

### 6️⃣ Create Service
Create a file `service.yaml`:

```
Apply:
```powershell
kubectl apply -f .\service.yaml
kubectl get svc
```
👉 **Why:** The service exposes the NGINX pods so they are accessible externally.

### 7️⃣ Access Application
```powershell
minikube service hello-service
```
or
```powershell
minikube ip
```
Visit `http://<minikube-ip>:<nodePort>`

### 8️⃣ Scale Deployment
```powershell
kubectl scale deployment hello-deployment --replicas=4
kubectl get pods
```
👉 **Why:** This tests Kubernetes' scaling capabilities.

### 9️⃣ Debugging and Logs
If issues occur:
- Check pod status:
  ```powershell
  kubectl get pods
  ```
- Describe pod:
  ```powershell
  kubectl describe pod <pod-name>
  ```
- View pod logs:
  ```powershell
  kubectl logs <pod-name>
  ```
- Check deployment events:
  ```powershell
  kubectl describe deployment hello-deployment
  ```
- Restart Minikube if cluster is unresponsive:
  ```powershell
  minikube stop
  minikube start
  ```

👉 **Common issues:**  
- Pod stuck in `ImagePullBackOff`: Check image name or your internet connection.  
- Service not accessible: Verify the `NodePort` is open and you’re using the correct IP.

### 10️⃣ Cleanup
```powershell
kubectl delete -f .\deployment.yaml
kubectl delete -f .\service.yaml
minikube stop
minikube delete
```

## 📸 Deliverables
- `deployment.yaml`
- `service.yaml`
- Screenshots:
  - `kubectl get pods`
  - `kubectl get svc`
  - Browser NGINX page
  - `kubectl describe deployment hello-deployment`
  - Output after scaling

## 💡 Outcome
✅ You will understand:
- Kubernetes components (pod, deployment, service)
- How to manage apps in Kubernetes
- How to debug and monitor applications in a local cluster
