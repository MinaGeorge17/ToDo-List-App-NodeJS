# ✅ ToDo List App – A Full DevOps Solution

This project illustrates how to build, containerize, and deploy a full-stack task management application using modern DevOps tools and practices. It showcases both Docker-based and Kubernetes-based deployment pipelines.


![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/0d6fde75db7418618ac35d7f4685da4e247ed19b/DevOps-assets/1.1%20Interface%20.png)



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



## ⚙️ Prerequisites

Before deploying the application, ensure the following system, software, and cloud prerequisites are in place.

### 🖥️ System Requirements

- **Operating System**
  - Local Machine: Ubuntu 20.04 (or compatible)
  - EC2 Instance: Ubuntu 20.04 (t3.small recommended)
- **Hardware**
  - AWS EC2 instance with at least 2 vCPUs and 2 GB RAM
- **Network**
  - Stable internet connection (required for GitHub, DockerHub, and AWS)

---

## 📦 Software Dependencies

Install the following tools on your local machine and/or EC2 instance:

- **Node.js and npm**  
  ```bash
  sudo apt update && sudo apt install nodejs npm -y
  ```

- **Git**  
  ```bash
  sudo apt install git -y
  ```

- **Docker (on EC2)**  
  ```bash
  sudo apt install docker.io -y
  ```

- **Ansible (on your local machine)**  
  ```bash
  sudo apt install ansible -y
  ```

- **AWS CLI**  
  ```bash
  sudo apt install awscli -y
  ```

- **MicroK8s (on EC2)**  
  ```bash
  sudo snap install microk8s --classic
  ```

- **Enable ArgoCD in MicroK8s**  
  ```bash
  microk8s enable argocd
  ```

## 📁 Repository and Registry

- **GitHub Repository**  
  [https://github.com/MinaGeorge17/ToDo-List-App-NodeJS](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS)

- **Docker Registry**  
  Hosted on Docker Hub as a private image (e.g., `minageorge17/todo-list-app:latest`)

- **Environment Variables (.env)**  
  ```env
  MONGODB_URI=your_mongodb_connection_string
  PORT=4000
  ```

  ## 🚧 Project Execution: Phase-by-Phase Breakdown

With the prerequisites in place, the project execution begins. Below is a structured breakdown of each major phase, walking through development, containerization, automation, and deployment — all aligned with modern DevOps principles. Each phase builds upon the previous, culminating in a fully automated, production-grade environment.

---

## 🧱 Phase 1: Cloning, Database Setup, Dockerization & CI Pipeline

This phase sets up the foundation of the ToDo List App by cloning the repo, configuring MongoDB, containerizing the app, and establishing a CI workflow using GitHub Actions.

---

### 🔁 Step 1: Clone the Repository

- Clone the project:
  ```bash
  git clone https://github.com/Ankit6098/Todo-List-nodejs

  ```

- Navigate into the project:
  ```bash
  cd Todo-List-App-nodejs
  ```

- List contents to verify:
  ```bash
  ls -a
  ```

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/0d6fde75db7418618ac35d7f4685da4e247ed19b/DevOps-assets/1.2%20App%20Interface%20.png)


---

### 🍃 Step 2: Set Up MongoDB Environment

If you don't have MongoDB installed locally, you can use **MongoDB Atlas** — a free, cloud-hosted database service.

#### 🧭 MongoDB Atlas Setup Instructions

1. Go to [https://www.mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas) and sign up for a free account.
2. Create a new **project** and then create a **free-tier cluster**.
3. After the cluster is provisioned:
   - Create a **new database user** with a **username and password**.
   - Go to **Network Access** → Allow access from anywhere (`0.0.0.0/0`).
   - Click **"Connect" → "Connect your application"** and copy the connection URI. It will look like this:

     ```
     mongodb+srv://<username>:<password>@cluster0.mongodb.net/?retryWrites=true&w=majority
     ```

4. Replace `<username>` and `<password>` with your actual credentials.

> ⚠️ This URI is private and includes credentials. Do **not** push it to GitHub.

---

#### 📁 Create Your `.env` File

- In the project root directory, create the environment file:
  ```bash
  touch .env
  ```

- Add the MongoDB connection string and port:
  ```bash
  echo "MONGODB_URI=your_mongodb_connection_string" >> .env
  echo "PORT=4000" >> .env
  ```

---

#### 🛡️ Protect Your Secrets

- Add `.env` to `.gitignore` to ensure it’s not tracked:
  ```bash
  echo ".env" >> .gitignore
  git add .gitignore
  git commit -m "Ignore .env for security"
  git push -u origin main
  ```

- Verify that `.env` is ignored:
  ```bash
  git status
  ```

---

#### ✅ Verify MongoDB Connection

- Run the app locally using Node or Docker:
  ```bash
  npm install
  npm start
  ```

  **OR if you're using Docker:**
  ```bash
  docker build -t todo-app .
  docker run -p 4000:4000 --env-file .env todo-app
  ```

- In your terminal logs, you should see a success message like:
  ```
  Connected to MongoDB...
  Server running on port 4000
  ```

- Visit the app in your browser at:
  ```
  http://localhost:4000/dashboard
  ```

If the dashboard loads and you can add tasks, the app is successfully connected to your MongoDB database.

---

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/0d6fde75db7418618ac35d7f4685da4e247ed19b/DevOps-assets/1.3%20adding%20a%20task%20.png)
![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/0d6fde75db7418618ac35d7f4685da4e247ed19b/DevOps-assets/1.4%20MongoDB%20success%20.png)




### 🐳 Step 3: Dockerize the Application

- Create a `Dockerfile` in the root directory (available in the repo).

- Build the Docker image:
  ```bash
  docker build -t todo-app .
  ```

- Run the app container locally:
  ```bash
  docker run -p 4000:4000 todo-app
  ```

- Check running containers:
  ```bash
  docker ps
  ```

- Commit and push the `Dockerfile`:
  ```bash
  git add Dockerfile
  git commit -m "Add Dockerfile for Dockerization"
  git push -u origin main
  ```
  
![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/0d6fde75db7418618ac35d7f4685da4e247ed19b/DevOps-assets/1.5%20image%20pushed%20dockerhub%20.png)

---

### ⚙️ Step 4: Set Up CI with GitHub Actions

- Create the workflows directory:
  ```bash
  mkdir -p .github/workflows
  ```

- Create a CI workflow file (`ci.yml`) – already included in the repository.

- Commit and push the workflow:
  ```bash
  git add .github/workflows/ci.yml
  git commit -m "Add CI pipeline with GitHub Actions"
  git push -u origin main
  ```

- Configure GitHub Actions Secrets:
  - `DOCKER_USERNAME`
  - `DOCKER_PASSWORD`  
  _(Set via GitHub → Repo → Settings → Secrets & Variables → Actions)_

- Check the Actions tab on GitHub for a successful workflow run.

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/0d6fde75db7418618ac35d7f4685da4e247ed19b/DevOps-assets/1.6%20GIT%20Actions%20workflow%20.png)

---

### ✅ Step 5: Validate Phase Completion

- Rebuild and test the Docker image:
  ```bash
  docker build -t todo-app .
  docker run -p 4000:4000 todo-app
  ```

- Visit [http://localhost:4000/dashboard](http://localhost:4000/dashboard) to confirm the app is running.

- Stop the running container:
  ```bash
  docker stop $(docker ps -q)
  ```

---

🎉 **Phase 1 completed:** The app is now containerized and CI is working with GitHub Actions and Docker Hub.



