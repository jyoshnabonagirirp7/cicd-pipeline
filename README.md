# CI/CD Pipeline with Jenkins, Docker Hub, Kubernetes, and ArgoCD

This repository demonstrates a complete CI/CD pipeline using **Jenkins**, **Docker**, **Docker Hub**, **Kubernetes**, and **ArgoCD**. It automates the build, test, and deployment of my application across environments using containerization and GitOps principles.

##  Project Architecture
GitHub (source code + k8s manifests)
↓
Jenkins (CI)
↓
Build & push Docker image to Docker Hub
↓
Update image tag in k8s/deployment.yaml
↓
Push updated manifest to GitHub
↓
ArgoCD (CD) watches repo and syncs with Kubernetes

##  Tools & Technologies Used

- **Jenkins** – For continuous integration and automation
- **Docker** – For containerizing the Node.js application
- **Docker Hub** – To store Docker images
- **Kubernetes** – Container orchestration using Minikube or EKS
- **ArgoCD** – For GitOps-based Continuous Deployment (installed via Helm)
- **GitHub** – Source code and deployment configuration management

-->
Jenkins CI Pipeline Steps
Pulls source code from GitHub

Builds a Docker image

Tags the image as <dockerhub-username>/node-app:latest

Pushes the image to Docker Hub

Updates the k8s/deployment.yaml with the new image version

Commits and pushes the updated file back to GitHub

-->
ArgoCD CD Pipeline
ArgoCD continuously watches the deployment.yaml file

When a new commit is detected, it syncs the Kubernetes cluster with the latest image

The application is automatically deployed or updated in the cluster

ArgoCD Installation & Access
1. Create ArgoCD Namespace
kubectl create namespace argocd
2.Add Argo Helm Repo and Install ArgoCD
helm install argocd argo/argo-cd --namespace argocd --set server.service.type=NodePort
3.Access ArgoCD UI
minikube service argocd-server -n argocd
4.Get ArgoCD Initial Admin Password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo
username is admin
5.create application in argocd UI based
6.Check ArgoCD application status:kubectl get applications -n argocd
7.Check your pods in default namespace:kubectl get pods -n default #argocd in this case


Access Your Application
kubectl get svc -n default
Get Minikube IP:minikube ip

Access your app in browser:

http://<minikube-ip>:<node-port>



Author
Jyoshna Bonagiri
