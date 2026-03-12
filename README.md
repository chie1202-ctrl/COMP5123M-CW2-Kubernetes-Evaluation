# COMP5123M-CW2-Kubernetes-Evaluation
Performance evaluation of Kubernetes (Kind vs K3s) for VNF deployment on Mac M4

This repository contains the experimental materials for Coursework 2, focusing on the performance comparison of Cloud-like and Edge-like Kubernetes environments for Virtual Network Function (VNF) deployment.

## 💻 Experimental Environment
- **Host Machine:** Mac M4 (Apple Silicon)
- **Hypervisor:** UTM (Apple Virtualization Framework)
- **Guest OS:** Ubuntu 22.04.5 LTS (ARM64)
- **Resource Constraints:** 2GB RAM, 2 vCPUs per VM

## 🛠 Kubernetes Distributions
1. **Cloud-like:** [Kind](https://kind.sigs.k8s.io/) (Kubernetes in Docker)
2. **Edge-like:** [K3s](https://k3s.io/) (Lightweight Kubernetes)

## 📦 VNF Selection
- **Workload:** Nginx (Alpine-based)
- **Role:** Emulating an API Gateway / Service Proxy in a 5G SBA context.

## 📂 Repository Structure
- `vnf-deployment.yaml`: The Kubernetes manifest used to deploy the Nginx VNF.
- `GenAI_troubleshooting.md`: Detailed logs of AI-assisted debugging and critical reflection on AI outputs.
- `results/`: Contains raw performance data obtained from Apache Benchmark (ab).
- `README.md`: Project overview and setup information.

## 📊 How to Reproduce
1. **Deploy VNF:** `kubectl apply -f vnf-deployment.yaml`
2. **Expose Service:** 
   - K3s: Use NodePort directly.
   - Kind: Use `kubectl port-forward --address 0.0.0.0 service/vnf-service 8080:80`
3. **Run Benchmark:** `ab -n 2000 -c 20 http://[Target-IP]:[Port]/`
