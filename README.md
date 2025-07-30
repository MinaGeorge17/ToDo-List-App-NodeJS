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
  - Start the application and access the interface using locahost:4000 :
  ```bash
  npm start
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


- In your terminal logs, you should see a success message like:
  ```
  Connected to MongoDB...
  Server running on port 4000
  ```

- Visit the app in your browser at:
  ```
  http://localhost:4000
  ```

> 🚀 **Success Check:** If the dashboard loads and you can add tasks, the app is successfully connected to your MongoDB database.

The following screenshots illustrate an example of adding a task (eg: buy your groceries) and then appears in the collections of MongoDB.



![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/0d6fde75db7418618ac35d7f4685da4e247ed19b/DevOps-assets/1.3%20adding%20a%20task%20.png)
![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/0d6fde75db7418618ac35d7f4685da4e247ed19b/DevOps-assets/1.4%20MongoDB%20success%20.png)

---


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

---



## 🚀 Phase 2: EC2 Instance Creation and Ansible Configuration

With the application containerized and a CI pipeline in place, we now move on to provisioning a virtual machine on AWS and configuring it using Ansible for remote automation.

---

### ☁️ Step 1: Launch AWS EC2 Instance

> **Goal**: Create a cloud-hosted virtual machine that will run our containerized application.

- Log into the [AWS Console](https://console.aws.amazon.com).
- Navigate to **EC2 > Instances > Launch Instance**.
- Configure the instance:
  - **AMI**: Ubuntu 20.04
  - **Instance Type**: `t3.small` (2 vCPUs, 2 GB RAM)
  - **Key Pair**: Create a new key pair (e.g., `todo-key.pem`)
  - **Security Group**:
    - Allow **SSH (22)** from your IP
    - Allow **TCP (31013)** for the app
    - Allow **TCP (8080)** for ArgoCD

> ⚠️ Save the `.pem` file securely and note your public EC2 IP.

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/053cbdb44d4b03c584c607f836ffd64f46237988/DevOps-assets/2.1%20Creating%20Linux%20EC2%20in%20aws.png)


---

### 🧱 Step 2: Install WSL for Windows (if applicable)

> **Goal**: Enable a Linux environment on Windows for Ansible execution.

```bash
wsl --install
```

Install Ubuntu from the Microsoft Store, then launch it and update the system:

```bash
sudo apt update && sudo apt upgrade -y
```

Verify installation:

```bash
wsl -l -v
```

---

### 🧰 Step 3: Install and Configure Ansible

> **Goal**: Use Ansible to remotely install Docker on the EC2 instance.

```bash
sudo apt update
sudo apt install ansible -y
```

Check Ansible version:

```bash
ansible --version
```

---

### 🔐 Step 4: Transfer Your EC2 Key to WSL

Move your `.pem` file to the Linux environment:

```bash
cp /mnt/c/Users/<YourUsername>/Downloads/todo-key.pem ~/
chmod 400 ~/todo-key.pem
```

---

### 🔌 Step 5: Verify SSH Access to EC2

```bash
ssh -i ~/todo-key.pem ubuntu@<ec2-public-ip>
```

Exit the EC2 shell after confirming access:

```bash
exit
```
![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/053cbdb44d4b03c584c607f836ffd64f46237988/DevOps-assets/2.2%20Successful%20SSH%20connection.png)

---

### 📂 Step 6: Add Ansible Inventory File

> The inventory file used for defining remote hosts and SSH details can be found in the repository as `inventory`.

Create it like this:

```bash
touch inventory
```

Edit it or copy it from the project repository.

---

### 📝 Step 7: Add Ansible Playbook

> The Ansible playbook that installs and starts Docker is included in the repository as `playbook.yml`.

Create it like this:

```bash
touch playbook.yml
```

Edit it or retrieve it from the repo.


![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/053cbdb44d4b03c584c607f836ffd64f46237988/DevOps-assets/2.3%20ansible%20env%20can%20connect%20to%20the%20ec2.png)

---

### 🧪 Step 8: Run the Playbook

```bash
ansible-playbook -i inventory playbook.yml
```
![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/053cbdb44d4b03c584c607f836ffd64f46237988/DevOps-assets/2.4%20ansible%20downloading%20docker%20on%20ec2%20ubuntu.png)

---

### ✅ Step 9: Validate Docker Installation on EC2

SSH into your EC2 instance:

```bash
ssh -i ~/todo-key.pem ubuntu@<ec2-public-ip>
```

Check Docker status:

```bash
sudo systemctl status docker
```

You should see `"active (running)"`.

Exit the session:

```bash
exit
```
![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/053cbdb44d4b03c584c607f836ffd64f46237988/DevOps-assets/2.5%20docker%20running%20on%20the%20ec2.png)

---

### 💾 Step 10: Commit Configuration Files

```bash
git add inventory ansible-playbook.yml
git commit -m "Add Ansible config and playbook for Docker setup"
git push -u origin main
```



## 🐳 Phase 3: Docker Compose Deployment with Auto-Updates

In this phase, we deployed the application using Docker Compose on the EC2 instance and configured **Watchtower** for automatic updates, enabling seamless continuous deployment without additional manual steps.

---

### 🧩 Step 1: Deploy the App with Docker Compose

> **Goal**: Use Docker Compose to run the containerized ToDo List App with health checks.

SSH into your EC2 instance:

```bash
ssh -i todo-key.pem ubuntu@<ec2-public-ip>
```

Ensure Docker Compose is installed (if not already):

```bash
sudo apt install docker-compose -y
```

Create the Compose file:

```bash
touch docker-compose.yml
```

> ✅ The full `docker-compose.yml` file is available in the repository. It includes port binding, health checks, and environment variables.

Start the app in detached mode:

```bash
docker-compose up -d
```

Check the status of running containers:

```bash
docker ps
```

Test the app locally on the instance:

```bash
curl http://localhost:31013
```

You should receive the app's HTML output.

---
![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/457d2f45364445482757d64c11cc1dfa72f64723/DevOps-assets/3.1%20Docker-compose%20running%20the%20app%20in%20the%20ec2.png)

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/457d2f45364445482757d64c11cc1dfa72f64723/DevOps-assets/3.2%20The%20application%20is%20running%20on%20the%20ec2%20successfully.png)




### 🔁 Step 2: Add Watchtower for Continuous Deployment (CD)

> **Goal**: Automatically detect and update containers when a new image is pushed to the Docker registry.

#### ✅ Why Watchtower?

Watchtower is a lightweight, Docker-native tool that **monitors running containers** and automatically pulls and redeploys the latest image versions. It’s a **zero-config CD solution**, ideal for simple, container-based setups where full GitOps is not required.

Compared to tools like **Portainer**, which offers a UI but requires manual intervention, or **Jenkins**, which demands more configuration and infrastructure, Watchtower provides:

- 📦 **Simplicity**: No need for pipeline scripting or external UI.
- ⚙️ **Automation**: Auto-restarts updated containers with zero downtime.
- 🚀 **Speed**: Quick to set up and integrates directly with Docker.

For this project, Watchtower complements the Docker Compose deployment by enabling **automatic container refresh** when the image is updated in Docker Hub — enabling **continuous deployment** with minimal setup.

---

#### 🛠️ Watchtower Setup

Pull the Watchtower image:

```bash
docker pull containrrr/watchtower
```

Run the Watchtower container:

```bash
docker run -d \
  --name watchtower \
  -v /var/run/docker.sock:/var/run/docker.sock \
  containrrr/watchtower
```

Check if Watchtower is running:

```bash
docker ps
```

(Optional) Run Watchtower with a scheduled interval (every 5 minutes):

```bash
docker stop watchtower
docker rm watchtower

docker run -d \
  --name watchtower \
  -v /var/run/docker.sock:/var/run/docker.sock \
  containrrr/watchtower \
  --schedule "*/5 * * * *"
```

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/457d2f45364445482757d64c11cc1dfa72f64723/DevOps-assets/3.3%20Docker-compose%20wroking%20after%20resolving%20the%20mongodb%20url%20problem%20and%20watch%20tower%20is%20set.png)

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/457d2f45364445482757d64c11cc1dfa72f64723/DevOps-assets/3.4%20pulling%20images%20to%20get%20anu%20update%20after%205%20mins%20the%20better%20one.png)

---

> ✅ With Watchtower in place, any image pushed to your registry will trigger an automatic update — delivering a true continuous deployment pipeline with minimal overhead.


### 🧪 Step 3: Test Auto-Update from Docker Registry

> **Goal**: Confirm Watchtower detects updated images and redeploys the container.

On your **local machine**, build and push an updated image:

```bash
docker build -t your_dockerhub_username/todo-app:latest .
docker push your_dockerhub_username/todo-app:latest
```

Return to your EC2 instance and monitor Watchtower logs:

```bash
docker logs watchtower
```

Look for logs indicating it pulled a new image and restarted the container.

---

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/457d2f45364445482757d64c11cc1dfa72f64723/DevOps-assets/3.5%20after%20changing%20in%20docker%20image%20to%20make%20sure%20it%20is%20pulling%20successfully.png)


### ✅ Step 4: Validate Phase 3 Completion

Confirm the Docker Compose services are healthy:

```bash
docker-compose ps
```

Optionally, test external access via browser or curl:

```bash
curl http://<ec2-public-ip>:31013
```

To clean up:

```bash
docker-compose down
docker stop watchtower
docker rm watchtower
```

Commit Docker Compose configuration:

```bash
git add docker-compose.yml
git commit -m "Add Docker Compose and Watchtower setup"
git push -u origin main
```

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/457d2f45364445482757d64c11cc1dfa72f64723/DevOps-assets/3.6%20connected%20to%20db%20as%20well.png)

---

> ✅ With this setup, the app is live and continuously updated via Docker Compose + Watchtower — a lightweight but powerful CD solution.



## 🚀 Phase 4: Kubernetes & ArgoCD Deployment (Bonus)

> In this final phase, we transitioned from Docker Compose to Kubernetes for orchestration, and introduced **ArgoCD** for GitOps-style Continuous Deployment. We used MicroK8s due to its lightweight nature and simplicity for single-node clusters like our EC2 instance.

---

### ⚙️ Why MicroK8s?

We chose **MicroK8s** because it's a lightweight, production-ready Kubernetes distribution that's perfect for single-node deployments on limited-resource VMs like EC2. It includes built-in support for add-ons like ArgoCD, DNS, and storage, making it ideal for small-scale DevOps projects.

---

### 💡 Step 1: Upgrade EC2 Instance Resources

To run Kubernetes efficiently, increase the EC2 instance type to at least `t3.small`.

- Stop the instance via AWS Console
- Go to: `Actions > Instance Settings > Change Instance Type`
- Choose `t3.small`, then start the instance again

SSH back in:

```bash
ssh -i todo-key.pem ubuntu@<your-ec2-ip>
```

Verify instance type (optional):

```bash
curl http://169.254.169.254/latest/meta-data/instance-type
```



---

### 🧱 Step 2: Install MicroK8s and Enable ArgoCD

Install and configure MicroK8s:

```bash
sudo snap install microk8s --classic
sudo usermod -a -G microk8s $USER
newgrp microk8s
```

Enable the required Kubernetes add-ons:

```bash
microk8s enable dns storage argocd
```

Check status and node readiness:

```bash
microk8s status
microk8s kubectl get nodes
```

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/008746415e856fa368fa4c9e081bb4f1a1a5b3f1/DevOps-assets/4.1%20microk8s%20-%20dashboard%20-%20dns%20enabled.png)

Updating the security group to add port range 30000-32767 for kubernetes.

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/008746415e856fa368fa4c9e081bb4f1a1a5b3f1/DevOps-assets/4.2%20security%20group%20updated%20for%20kubernetes.png)

---

### 📦 Step 3: Apply Kubernetes Manifests

Create a directory and apply Kubernetes manifests:

```bash
mkdir -p k8s
cd k8s
```

> 📝 The `deployment.yaml` and `service.yaml` files are located in the [k8s](./k8s) folder in this repository.

Apply the resources:

```bash
microk8s kubectl apply -f k8s/deployment.yaml
microk8s kubectl apply -f k8s/service.yaml
```

Verify deployment:

```bash
microk8s kubectl get deployments
microk8s kubectl get pods
```


![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/008746415e856fa368fa4c9e081bb4f1a1a5b3f1/DevOps-assets/4.3%20deployment%20and%20service%20yaml%20file%20done.png)



![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/008746415e856fa368fa4c9e081bb4f1a1a5b3f1/DevOps-assets/4.5%20application%20working%20in%20the%20pod.png)

---

### 🔄 Step 4: Configure ArgoCD

ArgoCD provides a GitOps-driven CD process where your Git repository is the single source of truth.

Create `.argocdignore` in the project root to target only Kubernetes manifests:

```bash
touch .argocdignore
```

Add these lines to it:

```
*
!k8s/deployment.yaml
!k8s/service.yaml
```

Commit and push:

```bash
git add .argocdignore k8s/
git commit -m "Add Kubernetes manifests and ArgoCD ignore file"
git push -u origin main
```

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/ed8cb5bad86b1bd4b22808d87dc3004e2512bc0b/DevOps-assets/4.6%20argocd%20downloaded.png)

Adding port 8080 in the security group of ec2 to access ArgoCD

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/ed8cb5bad86b1bd4b22808d87dc3004e2512bc0b/DevOps-assets/4.7%20adding%20port%208080%20to%20access%20argocd%20UI.png)


---

### 🌐 Step 5: Access ArgoCD Dashboard

Port-forward the ArgoCD server to access it in your browser:

```bash
ssh -i todo-key.pem -L 8080:localhost:8080 ubuntu@<your-ec2-ip> "microk8s kubectl port-forward -n argocd svc/argocd-server 8080:443"
```

Then open: [http://localhost:8080](http://localhost:8080)

Get the initial ArgoCD admin password:

```bash
microk8s kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

Login with username: `admin`

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/ed8cb5bad86b1bd4b22808d87dc3004e2512bc0b/DevOps-assets/4.8%20argocd%20is%20working%20successfully.png)

---

### ⚙️ Step 6: Create ArgoCD Application

In the ArgoCD dashboard:

- **App Name**: `todo-app`
- **Repo URL**: `https://github.com/MinaGeorge17/ToDo-List-App-NodeJS`
- **Path**: `k8s`
- **Cluster**: `https://kubernetes.default.svc`
- **Namespace**: `default`

Click **Create** and then **Sync** the application.


Saving the credentials of repo in ArgoCD as the repo was private to make ArgoCD able to access GITHUB.
![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/ed8cb5bad86b1bd4b22808d87dc3004e2512bc0b/DevOps-assets/4.10%20saving%20the%20credentials%20of%20the%20repo%20in%20argocd.png)

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/ed8cb5bad86b1bd4b22808d87dc3004e2512bc0b/DevOps-assets/4.11%20healthyyyy.png)



---

### ✅ Step 7: Validate the Kubernetes Deployment

Check pod status:

```bash
microk8s kubectl get pods
```

Test the application:

```bash
curl http://<your-ec2-ip>:31013/dashboard
```

Update and push a new Docker image (on your local machine):

```bash
docker build -t your_docker_username/todo-app:latest .
docker push your_docker_username/todo-app:latest
```

Sync from ArgoCD UI or CLI:

```bash
microk8s kubectl logs -l app=todo-app
```

Commit your final changes:

```bash
git add .
git commit -m "Deploy ToDo App on Kubernetes with ArgoCD"
git push
```

![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/ed8cb5bad86b1bd4b22808d87dc3004e2512bc0b/DevOps-assets/4.12%20%20.png)
![App UI](https://github.com/MinaGeorge17/ToDo-List-App-NodeJS/blob/ed8cb5bad86b1bd4b22808d87dc3004e2512bc0b/DevOps-assets/4.13%20.png)

---

✅ **You now have a fully GitOps-enabled Kubernetes deployment!**

### Contact
For any inquiries or collaboration, reach out at minaaziz6868@gmail.com


