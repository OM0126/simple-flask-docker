# Flask App using Docker

A simple Flask web application containerized using Docker and deployed on an AWS EC2 Ubuntu instance.

---

# Project Overview

This project demonstrates how to:

* Launch an AWS EC2 Ubuntu instance
* Connect to the EC2 instance using SSH
* Install Docker on Ubuntu
* Clone the project from GitHub
* Build a Docker image
* Run the Flask application inside a Docker container
* Configure the EC2 Security Group
* Access the application from a web browser
* Manage Docker images and containers
* Push the project to GitHub

---

# Tech Stack

* Python
* Flask
* Docker
* Ubuntu 22.04
* AWS EC2
* Git
* GitHub

---

# Project Structure

```text
flask-app-ecs/
├── app.py
├── run.py
├── requirements.txt
├── templates/
│   └── index.html
├── Dockerfile
└── README.md
```

---

# Step 1: Launch an EC2 Instance

* Launch an Ubuntu EC2 instance.
* Select the **t2.micro** instance type.
* Create or select an existing Key Pair.
* Allow **SSH (Port 22)** in the Security Group.
* Launch the instance.

---

# Step 2: Connect to the EC2 Instance

Navigate to the folder containing your key pair.

```bash
chmod 400 my-key.pem
```

Connect to the instance.

```bash
ssh -i my-key.pem ubuntu@<EC2-PUBLIC-IP>
```

---

# Step 3: Update Ubuntu

```bash
sudo apt update
sudo apt upgrade -y
```

---

# Step 4: Install Docker

Install Docker.

```bash
sudo apt install docker.io -y
```

Start Docker.

```bash
sudo systemctl start docker
```

Enable Docker.

```bash
sudo systemctl enable docker
```

Verify Docker installation.

```bash
docker --version
```

Check Docker status.

```bash
sudo systemctl status docker
```

---

# Step 5: Clone the Repository

```bash
git clone https://github.com/<username>/<repository-name>.git
```

```bash
cd flask-app-ecs
```

---

# Step 6: Build the Docker Image

Build the image.

```bash
sudo docker build -t flask-app .
```

Verify the image.

```bash
sudo docker images
```

---

# Step 7: Run the Docker Container

```bash
sudo docker run -d -p 80:80 --name flask-container flask-app
```

Verify the running container.

```bash
sudo docker ps
```

View logs.

```bash
sudo docker logs flask-container
```

---

# Step 8: Configure the EC2 Security Group

By default, only **SSH (Port 22)** is enabled. To access the Flask application from a browser, allow **HTTP (Port 80)**.

### Configure Inbound Rules

1. Open the **AWS Management Console**.
2. Navigate to **EC2**.
3. Select your EC2 instance.
4. Open the **Security** tab.
5. Click the attached **Security Group**.
6. Select **Edit Inbound Rules**.
7. Add the following rule:

| Type | Protocol | Port Range | Source               |
| ---- | -------- | ---------- | -------------------- |
| HTTP | TCP      | 80         | Anywhere (0.0.0.0/0) |

8. Save the changes.

---

# Step 9: Access the Application

Open your browser and visit:

```text
http://<EC2-PUBLIC-IP>
```

If the Docker container is running and Port **80** is allowed in the Security Group, the Flask application will load successfully.

---

# Useful Docker Commands

### Build Docker Image

```bash
sudo docker build -t flask-app .
```

### Run Docker Container

```bash
sudo docker run -d -p 80:80 --name flask-container flask-app
```

### List Docker Images

```bash
sudo docker images
```

### List Running Containers

```bash
sudo docker ps
```

### List All Containers

```bash
sudo docker ps -a
```

### View Container Logs

```bash
sudo docker logs <container-id>
```

### Stop a Container

```bash
sudo docker stop <container-id>
```

### Remove a Container

```bash
sudo docker rm <container-id>
```

### Remove an Image

```bash
sudo docker rmi <image-id>
```

---

# Git Commands

### Initialize Git Repository

```bash
git init
```

### Check Repository Status

```bash
git status
```

### Add Files

```bash
git add .
```

### Commit Changes

```bash
git commit -m "Initial commit"
```

### Rename Branch to Main

```bash
git branch -M main
```

### Add Remote Repository

```bash
git remote add origin https://github.com/<username>/<repository-name>.git
```

### Check Remote Repository

```bash
git remote -v
```

### Update Existing Remote

```bash
git remote set-url origin https://github.com/<username>/<repository-name>.git
```

### Push to GitHub

```bash
git push -u origin main
```

### Pull Latest Changes

```bash
git pull origin main
```

### Clone Repository

```bash
git clone https://github.com/<username>/<repository-name>.git
```

---

# Troubleshooting

## Dockerfile Build Error

If Docker cannot build the image because of an old Python version, replace:

```dockerfile
FROM python:3.7
```

with:

```dockerfile
FROM python:3.12-slim
```

---

## requirements.txt Not Found

Ensure the Dockerfile contains:

```dockerfile
COPY . .

RUN pip install -r requirements.txt
```

---

## Repository Already Exists

Check the current remote.

```bash
git remote -v
```

Update it if necessary.

```bash
git remote set-url origin https://github.com/<username>/<repository-name>.git
```

---

## Application Not Accessible in Browser

Check that:

* Docker container is running.
* Port **80** is mapped using `-p 80:80`.
* EC2 Security Group allows **HTTP (Port 80)**.
* You are using the correct **EC2 Public IP**.

---

# Future Improvements

* Push the Docker image to Amazon ECR.
* Deploy the application using Amazon ECS.
* Configure an Application Load Balancer.
* Add CI/CD using GitHub Actions.
* Monitor the application using Amazon CloudWatch.

---

# Learning Outcomes

After completing this project, you will learn:

* AWS EC2 fundamentals
* Connecting to Linux servers using SSH
* Installing Docker on Ubuntu
* Building Docker images
* Running Docker containers
* Configuring EC2 Security Groups
* Accessing containerized applications through a browser
* Git and GitHub workflow
* Preparing applications for cloud deployment

---

# Author

**OM**
