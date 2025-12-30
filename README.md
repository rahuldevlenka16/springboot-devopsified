# 🚀 SpringBoot DevOpsified

[![Maven](https://img.shields.io/badge/Build-Maven-C71A36?logo=apachemaven)](https://maven.apache.org/)
[![Docker](https://img.shields.io/badge/Container-Docker-2496ED?logo=docker)](https://www.docker.com/)
[![Terraform](https://img.shields.io/badge/IaC-Terraform-7B42BC?logo=terraform)](https://www.terraform.io/)
[![Helm](https://img.shields.io/badge/Deployment-Helm-0F1689?logo=helm)](https://helm.sh/)
[![Kubernetes](https://img.shields.io/badge/Orchestration-Kubernetes-326ce5?logo=kubernetes)](https://kubernetes.io/)
[![Argo CD](https://img.shields.io/badge/GitOps-Argo%20CD-FE5000?logo=argo)](https://argo-cd.readthedocs.io/)
[![Prometheus](https://img.shields.io/badge/Monitoring-Prometheus-E6522C?logo=prometheus)](https://prometheus.io/)
[![Grafana](https://img.shields.io/badge/Visualization-Grafana-F46800?logo=grafana)](https://grafana.com/)


> A unified **DevOpsified Spring Boot** monorepo featuring Maven, Docker, Terraform (EKS), Helm, Kubernetes, and Argo CD.



This is a **Unified monorepo** combining all DevOps layers — CI/CD, Docker, Terraform (EKS), Helm, and Kubernetes — for a Spring Boot application using my previous project https://github.com/rahuldevlenka16/spring_boot_todo_app

The old project consists of 

| Branch | Purpose |
|-------------|----------|
| `master` | Core Spring Boot application code |
| `docker` | Docker containerization setup |
| `cicd` | GitHub Actions workflows for CI/CD |
| `terraform` | Infrastructure-as-Code to provision AWS EKS cluster |
| `helm` | Helm chart for Kubernetes deployment, prometheus and grafana|
| `k8s` | Raw Kubernetes manifests |

All of these have now been **consolidated into a single monorepo**, for easier management, automation, and version control.

---

## 📝 Project Overview

This project consolidates multiple branches of a Spring Boot application into a **single monorepo**, covering:

- Application source code (Spring Boot)
- Containerization (Docker)
- CI/CD pipelines (GitHub Actions)
- Infrastructure provisioning (Terraform → AWS EKS)
- Kubernetes deployment (Helm)
- Continuous deployment via GitOps (Argo CD)

**Goal:** Demonstrate a full end-to-end DevOps workflow for a real-world Java application.

---

## 🏗 Architecture Diagram (High level)


<!-- <img width="1059" height="544" alt="image" src="https://github.com/user-attachments/assets/4226b70b-66d3-4248-aaf3-a1aaa6cb37be" /> -->
<!-- <img width="1153" height="536" alt="todo app diagram" src="https://github.com/user-attachments/assets/679a53aa-a0f9-4442-aa1e-44bb3d5ed92e" /> -->
<img width="2369" height="1101" alt="springboot devop" src="https://github.com/user-attachments/assets/c994613c-9091-42df-b18c-1ffc3c0377f9" /> 

This architecture shows the entire CI/CD process for deploying applications on Amazon EKS using GitHub Actions, Docker, Helm, and ArgoCD. When a user commits code to the GitHub repository, particularly the source code(src) and dockerfiles, the GitHub Actions pipeline is triggered. THe build job will build a Docker image and push it to Docker Hub with tag as per the last build ID. The update helm job will will then updates the Helm chart values (with the new image tag). ArgoCD continuously monitors this repository and automatically syncs any changes to the EKS cluster, ensuring the latest application version is deployed seamlessly without manual intervention into the EKS cluster.

  ## 🏗 Architecture Diagram (Detailed)
<img width="5002" height="2422" alt="4" src="https://github.com/user-attachments/assets/340d3f00-c115-452d-9233-09e6a298ec64" />

When a developer pushes code to GitHub, GitHub Actions automatically builds a Docker image, pushes it to Docker Hub, updates the Helm chart with the new image tag, and commits the change. ArgoCD continuously monitors the Helm chart repo and, when it detects the update, syncs the changes to the EKS cluster, ensuring the latest application version is deployed. Inside EKS, three application pods and one MySQL StatefulSet pod run as part of the workload, with the database pod using a Persistent Volume and Persistent Volume Claim backed by EBS for durable storage. Kubernetes Services expose the workloads: the Application Service uses a LoadBalancer to route external traffic, while the DB Service exposes MySQL internally to app pods. When a user sends a request, it hits the external LoadBalancer, flows to the AppService, then to one of the application pods, which queries the MySQL pod for data and receives the response from persistent storage. The application pod returns the final output through the LoadBalancer back to the user, enabling a fully automated, scalable, and production-grade deployment pipeline.

## ⚙️ Prerequisites

Before you begin, ensure you have the following installed:

- Java 8+ & Maven
- Docker
- kubectl
- Helm 
- Terraform
- AWS CLI (for EKS deployment)

---

## tools installation
  
    install git(refer docs)
    install docker(refer docs)
    
    instal kubectl:
      curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
      chmod +x kubectl
      sudo mv kubectl /usr/local/bin/
      kubectl --version
  
    install minikube:
    	curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    	sudo install minikube-linux-amd64 /usr/local/bin/minikube
    	minikube --version
  
  
    install helm:
      curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
    	helm version


## running the application(must install above tools first!)

    git clone https://github.com/rahuldevlenka16/springboot-devopsified
    cd springboot-devopsified/HelmChart/
    helm install test-app todoapp-chart/
    kubectl get pods
    kubectl get svc  
  <img width="953" height="128" alt="image" src="https://github.com/user-attachments/assets/4ab4f505-a5fb-429c-88b4-fe9a8b097a78" />


---

## CI in Github Actions
  <img width="1652" height="680" alt="image" src="https://github.com/user-attachments/assets/a3722760-704b-4f55-8ceb-8efedc17f545" />

## CD in Argo CD
  <img width="826" height="726" alt="image" src="https://github.com/user-attachments/assets/d8582afa-c79a-4c8b-b7f8-80ddfdaf8b84" />
  <img width="1733" height="816" alt="image" src="https://github.com/user-attachments/assets/f6163e27-0a15-4110-b072-5a9da9b66d68" />

## Monitoring
  <img width="1637" height="935" alt="image" src="https://github.com/user-attachments/assets/e1813a06-3242-4f0c-9ab6-95ebf3ec8889" />

  <img width="1779" height="939" alt="image" src="https://github.com/user-attachments/assets/ceb50eef-0881-464c-91e7-b7ec22f3daab" />



