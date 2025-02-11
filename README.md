# Deploying to EKS Cluster via Jenkins Pipeline

## Project Overview
I successfully implemented a Continuous Deployment (CD) pipeline that automatically deploys applications to an Amazon EKS cluster using Jenkins.

![Diagram](https://github.com/Princeton45/jenkins-eks-cd-pipeline/blob/main/images/diagram.png)

## Technologies Used
- Jenkins
- Amazon EKS (Elastic Kubernetes Service)
- Docker
- Kubernetes
- AWS IAM
- Linux

## Infrastructure Setup

### Jenkins Server
I set up a Linux-based Jenkins server with the following components:
- kubectl installation
- aws-iam-authenticator
- AWS credentials configuration  
- Kubeconfig file for EKS cluster connectivity

![Jenkins Dashboard](images/jenkins-dashboard.png)

### Amazon EKS Configuration
My EKS cluster runs with:
- 2 worker nodes
- Proper IAM roles and policies
- Configured security groups

![EKS Cluster](images/eks-cluster.png)

## Pipeline Implementation
I extended my existing Jenkins pipeline to include:
- AWS authentication
- EKS cluster connection
- Automated deployment to Kubernetes

![Pipeline Stages](images/pipeline-stages.png)

## Results
The pipeline successfully:
1. Authenticates with AWS
2. Connects to EKS cluster
3. Deploys applications automatically
4. Maintains zero-downtime deployments

![Kubernetes Dashboard](images/k8s-dashboard.png)

## Prerequisites
- AWS Account with EKS permissions
- Jenkins server
- Docker Hub account
- Basic understanding of Kubernetes

## Contact
[Your contact information]

![Project Demo](images/project-demo.png)

---
*Note: This project was completed as part of the Kubernetes on AWS - EKS module.*