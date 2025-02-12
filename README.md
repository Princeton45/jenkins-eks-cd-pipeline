# Deploying to EKS Cluster via Jenkins Pipeline

## Project Overview
I successfully implemented a Continuous Deployment (CD) pipeline that automatically deploys applications to an Amazon EKS cluster using Jenkins.

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
- Installed kubectl inside the Jenkins container

```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl; chmod +x ./kubectl; mv ./kubectl /usr/local/bin/kubectl
```
- Installed aws-iam-authenticator inside the Jenkins container

```bash
curl -Lo aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.6.11/aws-iam-authenticator_0.6.11_linux_amd64
chmod +x ./aws-iam-authenticator
mv ./aws-iam-authenticator /usr/local/bin
```

- Kubeconfig file for EKS cluster connectivity. This config file contains all the necessary information for authentication to the AWS Account & EKS Cluster.

![kube](https://github.com/Princeton45/jenkins-eks-cd-pipeline/blob/main/images/kube.png)

- Added AWS credentials configuration in Jenkins

![config](https://github.com/Princeton45/jenkins-eks-cd-pipeline/blob/main/images/config.png)



### Amazon EKS Configuration

![eks](https://github.com/Princeton45/jenkins-eks-cd-pipeline/blob/main/images/eks.png)


## Pipeline Implementation
I extended my existing Jenkins pipeline to include:
- AWS authentication
- EKS cluster connection
- Automated deployment to Kubernetes

```groovy
pipeline {   
    agent any
    tools {
        maven 'maven-3.9.9'
    }
    stages {
        stage("init") {
            steps {
                script {
                    echo "initializing..."
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    echo "building the application..."

                }
            }
        }

        stage("build image") {
            steps {
                script {
                    echo "building the docker image..."
                }
            }
        }

        stage("deploy") {
            environment {
                AWS_ACCESS_KEY_ID = credentials('jenkins_aws_access_key_id')
                AWS_SECRET_ACCESS_KEY = credentials('jenkins_aws_secret_access_key')
            }
            steps {
                script {
                   echo "deploying the docker image..."
                   sh "kubectl create deployment nginx-deployment --image=nginx"
                }
            }
        }               
    }
}
```

## Results
The Jenkins pipeline successfully:
1. Authenticates with AWS
2. Connects to EKS cluster
3. Deploys applications automatically

![done](https://github.com/Princeton45/jenkins-eks-cd-pipeline/blob/main/images/done.png)


