# 🚀 REALTIMEPROJECT – End-to-End DevOps CI/CD Pipeline

This project demonstrates a **complete real-time DevOps pipeline** using **Terraform, Jenkins, Ansible, Docker, Kubernetes (EKS), SonarQube, and Trivy**. It covers infrastructure provisioning, application build, containerization, image scanning, and automated deployment to Kubernetes.

---

## 📌 Project Overview

The goal of this project is to automate the **end-to-end lifecycle of a Java Spring Boot application**, starting from infrastructure creation to deployment on a Kubernetes cluster.

### High-Level Flow

```
Developer → GitHub → Jenkins → Maven → SonarQube → Docker → Trivy → DockerHub
                                                ↓
                                            Ansible
                                                ↓
                                          Kubernetes (EKS)
```

<img width="1277" height="701" alt="image" src="https://github.com/user-attachments/assets/558211f0-d11a-4630-b659-7081abfc4c84" />


---

## 🛠️ Tools & Technologies Used

| Category                 | Tools                           |
| ------------------------ | ------------------------------- |
| Cloud                    | AWS (EC2, VPC, Security Groups) |
| IaC                      | Terraform                       |
| CI/CD                    | Jenkins                         |
| Configuration Management | Ansible                         |
| Build Tool               | Maven                           |
| Containerization         | Docker                          |
| Container Registry       | DockerHub                       |
| Orchestration            | Kubernetes (EKS)                |
| Code Quality             | SonarQube                       |
| Security                 | Trivy                           |
| Language                 | Java (Spring Boot)              |

---

## 📂 Project Structure

```
REALTIMEPROJECT/
│
├── Terraform/
│   ├── main.tf
│   ├── outputs.tf
│   └── Install_Jenkins_Ansible_Docker.sh (optional)
│
├── Application/
│   ├── Dockerfile
│   ├── pom.xml
│   ├── application.properties
│   └── Jenkinsfile
│
├── Ansible/
│   ├── ansible_k8s_deploy_playbook.yaml
│   ├── deploy_docker.yaml
│   ├── k8s_deployment.yaml
│   └── hosts
│
└── README.md
```

---

## 🌍 Infrastructure Provisioning (Terraform)

Terraform is used to provision the AWS infrastructure:

### Resources Created

* Custom **VPC**
* **Public Subnet** with Internet Gateway
* **Route Table** and association
* **Security Groups**

  * Jenkins Server SG
  * Application Server SG
* **EC2 Instances**

  * Jenkins Server
  * Application Server
* **AWS Key Pair** for SSH access

### Jenkins EC2 Setup

Using `remote-exec`, the Jenkins instance installs:

* Jenkins
* Git, Maven
* Docker
* Ansible
* SonarQube (Docker container)
* Trivy

This enables Jenkins to act as the **CI/CD control node**.

---

## ⚙️ Application Layer

### Application Details

* Spring Boot Java application
* Built using **Maven**
* Exposes REST API
* Actuator & Prometheus enabled

### Dockerfile

* Uses OpenJDK 17 base image
* Copies built JAR
* Exposes port 8080
* Runs application using `java -jar`

---

## 🔄 Jenkins CI/CD Pipeline

The Jenkins pipeline automates the following stages:

1. **Checkout Code** – Pulls source code from GitHub
2. **Build** – Builds JAR using Maven
3. **SonarQube Scan** – Performs static code analysis
4. **Docker Build** – Builds Docker image with build number tag
5. **Trivy Scan** – Scans Docker image for vulnerabilities
6. **Docker Push** – Pushes image to DockerHub
7. **Manifest Update** – Updates Kubernetes deployment image tag
8. **Kubernetes Deployment** – Triggers Ansible playbook

---

## 🧩 Ansible Configuration Management

Ansible is used for **deployment automation**.

### Inventory (`hosts`)

Defines the target server:

```
[appserver]
<EC2_PUBLIC_IP>
```

---

### Kubernetes Deployment Playbook

**File:** `ansible_k8s_deploy_playbook.yaml`

This playbook:

1. Copies Kubernetes manifest to target server
2. Checks for kubeconfig file
3. Copies kubeconfig if missing
4. Applies Kubernetes deployment using `kubectl`

The variable `{{ playbook_dir }}` dynamically refers to the directory where the playbook exists, ensuring portability.

---

### Docker-Based Deployment (Optional)

**File:** `deploy_docker.yaml`

Used for non-Kubernetes deployments:

* Installs Docker
* Starts Docker service
* Runs container using `docker run`

⚠️ This file is **optional** and can be skipped when using Kubernetes.

---

## ☸️ Kubernetes Deployment

**File:** `k8s_deployment.yaml`

Resources Created:

* Deployment (2 replicas)
* LoadBalancer Service

The image tag is automatically updated by Jenkins to deploy the latest version.

---

## 🔐 Security & Quality

* **SonarQube** ensures code quality
* **Trivy** scans Docker images for vulnerabilities
* Credentials are managed securely using Jenkins credentials store

---

## ✅ Final Outcome

* Fully automated CI/CD pipeline
* Infrastructure provisioned using Terraform
* Secure, scalable Kubernetes deployment
* Zero manual intervention after code push

---

## 🎯 Use Cases

* DevOps fresher portfolio project
* Interview demonstration
* Real-time CI/CD learning reference
* GitHub showcase project

---
## ✅ Outputs & Results

### 🔹 Jenkins Pipeline Execution
<p align="center">
  <img src="https://github.com/user-attachments/assets/c656e2b7-547b-472f-b873-20e21ce0e877" />
" alt="Jenkins Pipeline Output" width="900">
</p>

---

⭐ If you like this project, don’t forget to star the repository!


