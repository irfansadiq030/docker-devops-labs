# Docker Fundamentals

This section documents the **fundamental concepts of Docker** and basic commands used to manage containers and images.  
Docker is a containerization platform that allows developers and system administrators to **build, package, and run applications in isolated environments called containers**.

Containers ensure that applications run the same way across different environments such as development, testing, and production.

## Docker Working & Terminology

Docker uses a **client-server architecture** to manage containers efficiently.  
Understanding the architecture helps in knowing how commands flow and how containers are created and managed.

**How it works:**
- You type commands in the **Docker CLI**
- Commands are sent to the **Docker Client**
- The **Docker Client** communicates with the **Docker Daemon** via REST API
- The **Docker Daemon** performs container operations such as building, running, and managing containers

---

### Docker Terminology

| Term | Explanation |
|------|-------------|
| **Docker Engine** | Complete platform installed on your system to build and run containers |
| **Docker Client** | CLI interface that communicates with the Docker Daemon |
| **Docker CLI** | Command-line tool used to run Docker commands like `docker run` |
| **Docker Daemon** | Background service that manages Docker objects (containers, images, volumes, networks) |
| **Docker Image** | Read-only template containing application, dependencies, and runtime |
| **Docker Container** | Running instance of a Docker image |
| **Docker Hub** | Public registry to store and retrieve Docker images |
| **Docker Volume** | Mechanism for persistent storage outside container filesystem |
| **Docker Network** | Virtual network allowing containers to communicate with each other and the outside world |

---

**In simple terms:**
1. You type commands in the CLI  
2. CLI sends them to Docker Client  
3. Client forwards commands to Docker Daemon via REST API  
4. Daemon builds or runs containers as requested  

> This architecture allows Docker to efficiently manage containers in an isolated and consistent environment.

## Installing Docker (Ubuntu)

To start working with Docker, we first need to install it on our system.  
This guide uses **Ubuntu 24.04 or later**.

---

### Step 1: Update System Packages

```bash
sudo apt update

### Step 2: Install Docker

```bash
sudo apt install docker.io -y

Explanation: Installs Docker Engine and Docker CLI on your system. The -y flag automatically confirms the installation prompt.

### Step 3: Start Docker Service

```bash
sudo systemctl start docker

Explanation: Starts the Docker daemon, the background service responsible for running containers and handling Docker commands.

### Step 4: Check Docker Status

```bash
sudo systemctl status docker

Explanation: You can confirm the status if docker is running or not.

### Step 5: Enable Docker to Start at Boot

```bash
sudo systemctl enable docker

Explanation: Ensures Docker starts automatically whenever your system reboots.

### Step 6: Add Current User to Docker Group (Optional)

```bash
sudo usermod -aG docker $USER

Explanation: Adds your user to the docker group so you can run Docker commands without using sudo.

### Step 6: Verify Docker Installation

```bash
docker version

Explanation: Displays the installed Docker client and Docker daemon versions to confirm a successful installation.

✅ Docker is now installed and ready to use! You can now pull images and run containers.
