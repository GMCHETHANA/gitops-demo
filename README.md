# GitOps Demo
This repository demonstrates a GitOps workflow using Kubernetes and Argo CD. It contains Kubernetes manifests for deploying an example application and an Argo CD Application manifest to automate deployment.

# Project Structure
.
├── argo-cd/            # Argo CD Application manifests
│   └── app.yaml
├── k8s/                # Kubernetes resources
│   ├── configmap.yaml
│   ├── deployment.yaml
│   └── service.yaml
└── README.md           # Project documentation

# Prerequisites
- Kubernetes cluster (e.g., Minikube, Kind, or cloud provider)
- Argo CD installed in the cluster
- kubectl CLI installed
- (Optional) argocd CLI for interacting with Argo CD

# Usage
1) Apply Kubernetes manifests manually (optional if using Argo CD):
kubectl apply -f k8s/

2) Deploy the application via Argo CD:
   kubectl apply -f argo-cd/app.yaml -n argocd
   
3) Access Argo CD Web UI (optional):
   kubectl port-forward svc/argocd-server -n argocd 8080:443
Open your browser at https://localhost:8080 and log in using the initial admin credentials:
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode

4) Sync the application via CLI (optional):
   argocd login localhost:8080 --username admin --password <password> --insecure
argocd app sync gitops-demo-app

# Notes
- This project demonstrates pure GitOps, where the Git repository is the single source of truth. Any changes to the manifests in Git will automatically be reflected in the cluster via Argo CD.
- Only the essential GitOps manifests are tracked; large files like Terraform binaries or CLI installers are excluded to keep the repository clean.

