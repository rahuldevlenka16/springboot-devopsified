# 🚀 SpringBoot DevOpsified

[![Maven](https://img.shields.io/badge/Build-Maven-C71A36?logo=apachemaven)](https://maven.apache.org/)
[![Docker](https://img.shields.io/badge/Container-Docker-2496ED?logo=docker)](https://www.docker.com/)
[![Terraform](https://img.shields.io/badge/IaC-Terraform-7B42BC?logo=terraform)](https://www.terraform.io/)
[![Helm](https://img.shields.io/badge/Deployment-Helm-0F1689?logo=helm)](https://helm.sh/)
[![Kubernetes](https://img.shields.io/badge/Orchestration-Kubernetes-326ce5?logo=kubernetes)](https://kubernetes.io/)
[![Argo CD](https://img.shields.io/badge/GitOps-Argo%20CD-FE5000?logo=argo)](https://argo-cd.readthedocs.io/)


> A unified **DevOpsified Spring Boot** monorepo featuring Maven, Docker, Terraform (EKS), Helm, Kubernetes, and Argo CD.



This is a **Unified monorepo** combining all DevOps layers — CI/CD, Docker, Terraform (EKS), Helm, and Kubernetes — for a Spring Boot application using my previous project https://github.com/rahuldevlenka16/spring_boot_todo_app

The old project consists of 

| Branch | Purpose |
|-------------|----------|
| `master` | Core Spring Boot application code |
| `docker` | Docker containerization setup |
| `cicd` | GitHub Actions workflows for CI/CD |
| `terraform` | Infrastructure-as-Code to provision AWS EKS cluster |
| `helm` | Helm chart for Kubernetes deployment |
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

## 🏗 Architecture Diagram


<!-- <img width="1059" height="544" alt="image" src="https://github.com/user-attachments/assets/4226b70b-66d3-4248-aaf3-a1aaa6cb37be" /> -->
<!-- <img width="1153" height="536" alt="todo app diagram" src="https://github.com/user-attachments/assets/679a53aa-a0f9-4442-aa1e-44bb3d5ed92e" /> -->
<img width="2369" height="1101" alt="springboot devop" src="https://github.com/user-attachments/assets/c994613c-9091-42df-b18c-1ffc3c0377f9" />

  


This architecture shows the entire CI/CD process for deploying applications on Amazon EKS using GitHub Actions, Docker, Helm, and ArgoCD. When a user commits code to the GitHub repository, the GitHub Actions pipeline is triggered. THe build job will build a Docker image and push it to Docker Hub with tag as per the last build ID. The update helm job will will then updates the Helm chart values (with the new image tag). ArgoCD continuously monitors this repository and automatically syncs any changes to the EKS cluster, ensuring the latest application version is deployed seamlessly without manual intervention into the EKS cluster.
---

## ⚙️ Prerequisites

Before you begin, ensure you have the following installed:

- Java 8+ & Maven
- Docker
- kubectl
- Helm 
- Terraform
- AWS CLI (for EKS deployment)

---




