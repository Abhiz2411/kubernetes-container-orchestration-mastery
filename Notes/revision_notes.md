# Kubernetes Notes for Beginners 🚀

## 📚 Key Concepts

### 1️⃣ Kubernetes Architecture
- **Master Node**:
  - Controls and manages the cluster.
  - Key components: API Server, Controller Manager, Scheduler, etcd.
- **Worker Nodes**:
  - Run application workloads.
  - Key components: Kubelet, Kube Proxy, Pods.

### 2️⃣ Core Components
- **Pod**:
  - Smallest deployable unit.
  - Contains one or more containers.
- **Service**:
  - Exposes an application running on a set of Pods.
  - Types: ClusterIP, NodePort, LoadBalancer, ExternalName.
- **Deployment**:
  - Manages the deployment and scaling of Pods.
  - Enables Rolling Updates and Rollbacks.
- **ConfigMap & Secret**:
  - ConfigMap: Stores non-sensitive configuration data.
  - Secret: Stores sensitive information securely.

### 3️⃣ Common Objects
- **Namespace**:
  - Isolates resources within a cluster.
- **Ingress**:
  - Manages external HTTP/S access to services.
- **Volume**:
  - Persistent storage for Pods.
- **ReplicaSet**:
  - Ensures a specified number of Pod replicas are running.

---

## 🔧 Frequently Used Commands

### 🏗️ Cluster Setup
```bash
# Initialize Kubernetes Cluster (Master Node)
sudo kubeadm init --pod-network-cidr=192.168.0.0/16

# Set up kubeconfig for current user
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Apply network plugin (e.g., Calico)
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

# Join Worker Node to Cluster
kubeadm join <MASTER_IP>:6443 --token <TOKEN> --discovery-token-ca-cert-hash <HASH>
```

### 🛠️ Resource Management
```bash
# Create Resources
kubectl create -f <file>.yaml

# Apply Changes
kubectl apply -f <file>.yaml

# Get Resources
kubectl get pods
kubectl get services
kubectl get deployments

# Describe Resources
kubectl describe pod <pod_name>
kubectl describe service <service_name>

# Delete Resources
kubectl delete -f <file>.yaml
kubectl delete pod <pod_name>
kubectl delete deployment <deployment_name>
```

### 🚀 Deployment
```bash
# Create a Deployment
kubectl create deployment <deployment_name> --image=<image_name>

# Scale Deployment
kubectl scale deployment <deployment_name> --replicas=<number>

# Update Deployment (Rolling Update)
kubectl set image deployment/<deployment_name> <container_name>=<new_image>

# Rollback Deployment
kubectl rollout undo deployment/<deployment_name>
```

### 🕵️‍♂️ Debugging
```bash
# View Logs
kubectl logs <pod_name>

# Get Detailed Pod Info
kubectl describe pod <pod_name>

# Access Pod Shell
kubectl exec -it <pod_name> -- /bin/bash

# View Events
kubectl get events
```

### 📦 Configurations
```bash
# Create ConfigMap
kubectl create configmap <config_name> --from-literal=<key>=<value>

# Create Secret
kubectl create secret generic <secret_name> --from-literal=<key>=<value>

# View ConfigMap/Secret
kubectl get configmap
kubectl get secret

# Describe ConfigMap/Secret
kubectl describe configmap <config_name>
kubectl describe secret <secret_name>
```

### 🖧 Networking
```bash
# Expose Pod as Service
kubectl expose pod <pod_name> --type=NodePort --port=<port>

# Get Service Info
kubectl get svc

# Apply Ingress
kubectl apply -f <ingress_file>.yaml
```

### 📜 YAML Template Basics
```yaml
# Deployment Example
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: example-app
  template:
    metadata:
      labels:
        app: example-app
    spec:
      containers:
      - name: example-container
        image: nginx:latest
        ports:
        - containerPort: 80
```

---

## 🌐 Useful Links
- 🌐 [Portfolio](https://abhijit-zende.vercel.app/)
- ✍️ [Hashnode Blog](https://abhijitzende.hashnode.dev/)

Happy Learning Kubernetes! 🚀
