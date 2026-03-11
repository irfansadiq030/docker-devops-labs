# Deploying a Flask-Based Python App on AWS EC2 using Docker + Push to Docker Hub

## 🏭 Industry Scenario

A retail analytics company is developing a lightweight **internal dashboard tool** for its field agents to check the latest store audit summaries. The first version of this application is a simple **Python Flask web app** that runs on **port 8000** and does not require a database.

The goal is to **rapidly deploy this tool on an AWS EC2 instance using Docker**, ensuring that it can be easily deployed, scaled, and maintained across different environments.

---

## 🎯 Objective

This lab demonstrates how to:

* Deploy a **Python Flask application** on an AWS EC2 instance
* Containerize the application using **Docker**
* Expose the application through proper **port mapping**
* Configure **AWS Security Groups**
* Push the Docker image to **Docker Hub** for portability and version control

---

# Step-by-Step Implementation

---

# Part 1 — Run the Application Manually on EC2

This section demonstrates how the application runs **without Docker**, which helps understand the environment setup.

---

## Step 0: Launch an Ubuntu EC2 Instance

1. Open **AWS Console**
2. Navigate to **EC2 → Launch Instance**

Configuration:

* **AMI:** Ubuntu 22.04 LTS
* **Instance Type:** t2.micro
* **Key Pair:** Create or choose an existing key pair
* **Security Group Rules:**

  * SSH → Port **22**
  * Custom TCP → Port **8000**

Launch the instance and note the **Public IPv4 Address**.

---

## Step 1: Connect to EC2 via SSH

```bash
ssh -i "your-key.pem" ubuntu@ec2-your-ip.compute.amazonaws.com
```

### Explanation

* `ssh` → Secure Shell used to connect to remote machines
* `-i` → Specifies the private key file
* `ubuntu` → Default username for Ubuntu EC2 instances
* `ec2-your-ip` → Public IP or DNS of your EC2 instance

---

## Step 2: Clone the Flask Application Repository

```bash
git clone https://github.com/Umair1012/Flask-Based-Python-Application-on-AWS-EC2-with-Docker.git
```

### Explanation

This command downloads the Flask application source code from GitHub to your EC2 instance.

Move into the project directory:

```bash
cd Flask-Based-Python-Application-on-AWS-EC2-with-Docker
```

---

## Step 3: Install Python and pip

```bash
sudo apt update
sudo apt install python3-pip -y
```

### Explanation

* `apt update` → Updates package list
* `python3-pip` → Installs Python package manager
* `-y` → Automatically confirms installation

---

## Step 4: Create a Virtual Environment

```bash
python3 -m venv venv
```

### Explanation

Creates an isolated Python environment to manage dependencies separately from the system Python.

---

## Step 5: Activate the Virtual Environment

```bash
source venv/bin/activate
```

### Explanation

Activates the virtual environment so all Python packages install locally inside it.

---

## Step 6: Install Dependencies

```bash
pip install -r requirements.txt
```

### Explanation

Installs all required Python packages listed in the `requirements.txt` file.

---

## Step 7: Run the Flask Application

```bash
python app.py
```

Your application will start on **port 8000**.

Open in browser:

```
http://<EC2-PUBLIC-IP>:8000
```

---

# Part 2 — Run the Application using Docker

Now we will **containerize the application using Docker**.

---

## Step 1: Install Docker on EC2

```bash
sudo apt install docker.io -y
```

Start Docker service:

```bash
sudo systemctl start docker
```

Enable Docker at system startup:

```bash
sudo systemctl enable docker
```

Verify installation:

```bash
docker --version
```

---

## Step 2: Create a Dockerfile

Create a file named **Dockerfile** inside the project directory.

```
Dockerfile
```

### Dockerfile Content

```dockerfile
# Use lightweight Python base image
FROM python:3.10-slim

# Set working directory
WORKDIR /app

# Copy application files
COPY . .

# Install Python dependencies
RUN pip install -r requirements.txt

# Expose application port
EXPOSE 8000

# Start the Flask application
CMD ["python", "app.py"]
```

### Explanation

| Instruction | Purpose                                    |
| ----------- | ------------------------------------------ |
| FROM        | Specifies the base image                   |
| WORKDIR     | Sets working directory inside container    |
| COPY        | Copies project files into container        |
| RUN         | Executes commands during build             |
| EXPOSE      | Declares application port                  |
| CMD         | Runs the application when container starts |

---

## Step 3: Build the Docker Image

```bash
docker build -t flask-audit-app:latest .
```

### Explanation

* `docker build` → Builds a Docker image
* `-t` → Tags the image
* `flask-audit-app:latest` → Image name and version
* `.` → Build context (current directory)

Example output:

```
Successfully built abc123
Successfully tagged flask-audit-app:latest
```

---

## Step 4: Push Image to Docker Hub

Login to Docker Hub:

```bash
docker login
```

Tag the image:

```bash
docker tag flask-audit-app:latest your_dockerhub_username/flask-audit-app:v1
```

Push image:

```bash
docker push your_dockerhub_username/flask-audit-app:v1
```

### Explanation

This uploads the Docker image to **Docker Hub**, allowing it to be reused on any server.

---

## Step 5: Run the Docker Container

```bash
docker run -d -p 8000:8000 your_dockerhub_username/flask-audit-app:v1
```

### Explanation

| Option         | Meaning                         |
| -------------- | ------------------------------- |
| `docker run`   | Creates and runs container      |
| `-d`           | Run container in background     |
| `-p 8000:8000` | Map host port to container port |
| image name     | Docker image to run             |

Check running containers:

```bash
docker ps
```

---

## Step 6: Remove Docker Image (Optional)

```bash
sudo docker rmi -f <image-id>
```

### Explanation

Deletes a Docker image from the local system.

---

# Step 7 — Configure Security Group

Open **AWS EC2 → Security Groups → Inbound Rules**

Add rule:

| Type       | Port | Source    |
| ---------- | ---- | --------- |
| Custom TCP | 8000 | 0.0.0.0/0 |

This allows external users to access the application.

---

# Step 8 — Test the Application

Open browser and visit:

```
http://<EC2-PUBLIC-IP>:8000
```

Expected output:

```
Welcome to the Internal Audit Dashboard - Version 1
```

Your Flask application is now running successfully inside a Docker container on AWS EC2.

---

# Conclusion

This lab demonstrates how a lightweight application can be **containerized and deployed using industry-standard tools such as Flask, Docker, and AWS EC2**.

By pushing the Docker image to Docker Hub, the application becomes **portable, version-controlled, and easily deployable across different environments**.

### Industry Impact

This workflow can later be integrated with **CI/CD tools such as Jenkins or GitHub Actions**, enabling automated build and deployment pipelines for faster and more reliable software delivery.

---
