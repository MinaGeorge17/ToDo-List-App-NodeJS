# ✅ ToDo List App – A Full DevOps Solution

This project illustrates how to build, containerize, and deploy a full-stack task management application using modern DevOps tools and practices. It showcases both Docker-based and Kubernetes-based deployment pipelines.

[!App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/6234c4e8f8af8841b13b8732576482183e5d1cae/DevOps-assets/1.1%20App%20Interface%20.png)

## 🧭 Project Overview

The ToDo List App is a DevOps-powered task management solution designed to exemplify scalable, automated software delivery workflows. Built with Node.js and backed by MongoDB, it allows users to perform full CRUD operations through a responsive web interface.

Deployed on an AWS EC2 instance, the project offers **two deployment strategies**:

- **Docker Compose** with **Watchtower** for simple container orchestration and automatic updates.
- **Kubernetes (MicroK8s)** with **ArgoCD** for a declarative, GitOps-based deployment approach.

It leverages **GitHub Actions** for continuous integration, **Ansible** for provisioning and configuration, and **Docker** for containerization—forming a complete CI/CD pipeline. Accessible via the EC2 instance’s public IP, the solution demonstrates real-world automation, health monitoring, and production-readiness in a cloud-native setup.



## 📚 Project Phases

The project is structured into four progressive phases, each building upon the previous to form a complete and production-grade DevOps workflow:

### Phase 1: Application Containerization and CI Integration
- Clone the repository and configure environment variables for MongoDB connectivity.
- Containerize the Node.js application using Docker.
- Set up a CI pipeline using GitHub Actions to automatically build and push Docker images to DockerHub.

### Phase 2: Infrastructure Provisioning and Configuration
- Launch a Linux-based virtual machine on AWS EC2.
- Use Ansible from a local control machine to automate the provisioning of essential packages such as Docker, Git, Node.js, and MongoDB on the EC2 instance.

### Phase 3: Docker-Based Deployment and Auto-Update
- Deploy the containerized application using Docker Compose.
- Configure health checks and implement automatic image updates using Watchtower.
- Ensure the application remains highly available and restartable with minimal manual intervention.

### Phase 4: Kubernetes Orchestration and GitOps Deployment
- Replace Docker Compose with a Kubernetes-based deployment using MicroK8s.
- Manage application deployment using GitOps practices through ArgoCD.
- Use secrets, services, deployments, and ingress controllers to simulate real-world production deployments on cloud-native infrastructure.

## 🛠️ Tools Used

The development and deployment of this project utilized a wide range of modern DevOps tools and technologies to create a reliable, scalable, and fully automated pipeline:

- **Node.js & Express.js** – Backend runtime and web framework for building the application logic.
- **EJS** – Templating engine used for rendering dynamic HTML views.
- **MongoDB & Mongoose** – NoSQL database and object data modeling (ODM) library for task persistence.
- **Nodemon** – Development utility for monitoring file changes and restarting the server automatically.
- **Docker** – Container platform for packaging the application and managing isolated environments.
- **Git & GitHub** – Version control and remote repository for code collaboration and CI/CD workflows.
- **GitHub Actions** – Continuous Integration (CI) tool for automating Docker builds and image pushes.
- **Ansible** – Configuration management tool for automating software setup on the VM.
- **AWS EC2 (t3.small)** – Cloud-based virtual machine used as the host environment for deployment.
- **Docker Compose** – Used for initial multi-container orchestration and local testing.
- **Watchtower** – Lightweight service for Continuous Deployment (CD) by monitoring and updating Docker containers automatically.
- **MicroK8s** – Lightweight, production-grade Kubernetes distribution used for container orchestration.
- **kubectl** – Command-line interface for managing Kubernetes clusters.
- **ArgoCD** – GitOps-based continuous deployment system for declarative application management on Kubernetes.
- **curl** – Command-line tool for HTTP requests, used for service testing and debugging.

