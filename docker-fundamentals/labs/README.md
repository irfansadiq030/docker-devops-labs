# Lab 1: Run Nginx Container

🏭 **Industry Scenario:**  
You're a Cloud Administrator at a company named **DevOpsMart**. The development team asks you to set up and run a **containerized Nginx web server** using Docker. Your task is to pull the image from Docker Hub, run the container, manage it, and ensure it’s working as expected.

🧠 **Objective:**  
This lab provides hands-on experience with Docker by guiding you through the complete lifecycle of a containerized application—from installation to deployment and management—using a real-world example. It builds foundational skills in **containerization, Docker architecture, and image/container operations**.

---

### Step 1: Pull Nginx Image
```bash
docker pull nginx
```
Explanation: Downloads the official Nginx image from Docker Hub to your local system.

### Step 2: List Local Images
```bash
docker images
```
Explanation: Shows all images available locally

### Step 3: Run Nginx Container
```bash
docker run -d -p 8080:80 --name webserver nginx
```
Explanation:
* docker run : This is the base command to start a container from an image.
* -d (detached mode) : -d stands for detached mode. Normally, when you run a container, Docker shows all logs in your terminal, and your terminal is “busy” with that container. Detached mode means: run the container in the background and free your terminal.
* -p 8080:80 (port mapping): This tells Docker how to connect the container to your computer.
* --name webserver (container name): By default, Docker gives containers random names like jolly_turing. --name webserver lets you give a friendly name to your container.
* nginx (image): This is the Docker image you want to run.

### Step 4: List Running Containers
```bash
docker ps
```
Explanation: Shows all containers currently running. 

### Step 5: Test in Browser
Open: http://localhost:8080

### Step 6: Stop Container
```bash
docker stop webserver
```
Explanation: Stops the container.

### Step 7: Remove Container
```bash
docker rm webserver
```
Explanation: Deletes the stopped container.

### Step 8: Check Container Logs
```bash
docker run -d -p 8080:80 --name webserver nginx
docker logs webserver
```
Explanation: View logs for troubleshooting or verifying container activity.

✅ Lab Complete: You have successfully pulled, ran, and managed your first Docker container!