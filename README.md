# Docker Practice
# Docker Journey – Setup, Troubleshooting & Application Deployment

## Overview

This repository documents my complete Docker learning and setup journey, including:

* Docker basics and concepts
* Local setup attempts on macOS Catalina
* Troubleshooting virtualization and Docker installation issues
* Switching to GitHub Codespaces
* Building and Dockerizing a Python Flask application
* Using Docker Compose
* Pushing images to Docker Hub

---

# System Information

* Device: MacBook Pro
* OS: macOS Catalina 10.15.7
* Processor: Intel Core i5 (Dual Core)

---

# Initial Goal

The task was to:

1. Create a simple web application
2. Dockerize the application
3. Build and run Docker containers
4. Push Docker image to Docker Hub
5. Learn and use Docker Compose

---

# Docker Learning Notes

During this journey, I learned:

* Difference between Docker Image and Container
* Dockerfile instructions
* Port binding
* Docker networking
* Docker volumes
* Docker Compose
* Image tagging and pushing to Docker Hub
* Difference between Docker and Virtual Machines

A separate `NOTES.md` file contains my detailed learning notes.

---

# Local Docker Setup Attempts on macOS

## Attempt 1 – Docker Desktop

### What I Tried

* Tried installing Docker Desktop directly on macOS Catalina.

### Issue Faced

* Docker Desktop versions were not properly supported on macOS Catalina.
* Compatibility issues occurred.

### Result

❌ Docker Desktop setup was unsuccessful.

---

# Attempt 2 – Colima + Lima

## What I Tried

Installed:

* Colima
* Lima

Commands used:

```bash
colima start
```

## Issues Faced

### Error:

```bash
FATA[0000] lima compatibility error: error checking Lima version: exec: "limactl": executable file not found in $PATH
```

### Additional Issues

* Manual Lima installation problems
* Corrupted archive download
* Virtualization framework compatibility issues on Catalina

### Error:

```bash
dyld: Library not loaded: /System/Library/Frameworks/Virtualization.framework
```

## Result

❌ Colima + Lima approach failed due to macOS compatibility limitations.

---

# Attempt 3 – VirtualBox

## What I Tried

* Installed VirtualBox 6.1.x
* Created Ubuntu virtual machine

## Issues Faced

### Kernel Driver Errors

```bash
Kernel driver not installed (rc=-1908)
```

### VBox Driver Missing

```bash
VBoxDrv.kext failed to load
```

### VM Startup Failure

```bash
The virtual machine 'Ubuntu' has terminated unexpectedly during startup
```

## Troubleshooting Done

* Allowed Oracle permissions in Security & Privacy
* Tried loading kernel extensions manually
* Reinstalled VirtualBox multiple times
* Tried different versions

## Result

❌ VirtualBox was unable to run virtual machines on macOS Catalina.

---

# Attempt 4 – VMware & UTM

## VMware

* Tried exploring VMware Fusion
* Faced compatibility and download access limitations

## UTM

* Installed multiple UTM versions
* Catalina compatibility issues occurred

### Error

```bash
Application requires macOS 11.3 or later
```

## Result

❌ Alternative virtualization tools were also unsuccessful.

---

# Final Solution – GitHub Codespaces

Since local virtualization and Docker setup were failing on macOS Catalina, I switched to:

* GitHub Codespaces

This provided:

* Linux environment
* Docker support
* Cloud-based development environment
* Easy GitHub integration

---

# Application Development

## Technology Used

* Python
* Flask

## Application Features

* Basic Flask web application
* Multiple routes
* Runs on port 5000

---

# Dockerizing the Application

## Dockerfile Created

```Dockerfile
FROM python:3.9

WORKDIR /app

COPY app/ /app

RUN pip install -r requirements.txt

CMD ["python", "app.py"]
```

## Concepts Learned

* Base image
* Working directory
* Copying files
* Installing dependencies
* Running containers

---

# Building Docker Image

## Command Used

```bash
docker build -t my-python-app .
```

## Result

✅ Docker image built successfully.

---

# Running Docker Container

## Command Used

```bash
docker run -p 5000:5000 my-python-app
```

## Result

✅ Container started successfully.

Application output:

```text
Hello from Docker!
```

---

# Docker Hub Integration

## Steps Performed

### Login

```bash
docker login
```

### Tag Image

```bash
docker tag my-python-app pranavcodes1/sample-app
```

### Push Image

```bash
docker push pranavcodes1/sample-app
```

## Result

✅ Image successfully pushed to Docker Hub.

Docker Hub Repository:

```text
https://hub.docker.com/r/pranavcodes1/sample-app
```

---

# Docker Compose

## docker-compose.yml

```yaml
version: '3'

services:
  web:
    image: pranavcodes1/sample-app
    ports:
      - "5000:5000"
```

## Command Used

```bash
docker compose up
```

## Result

✅ Application successfully ran using Docker Compose.

---

# GitHub Repository

Repository Link:

```text
https://github.com/PranavCodes1/docker-practice
```

---

# Screenshots / Outputs

## Suggested Screenshots to Add

Add screenshots of:

1. Flask application running
2. Docker image build success
3. Docker container running
4. Docker Compose running
5. Docker Hub repository
6. GitHub repository structure
7. Docker commands output

---

# Key Learnings

## Technical Learnings

* Docker fundamentals
* Container lifecycle
* Docker images and containers
* Dockerfile instructions
* Docker networking
* Docker Compose usage
* Docker Hub workflow

## Practical Learnings

* Troubleshooting setup issues
* Understanding virtualization limitations on macOS Catalina
* Using cloud development environments
* GitHub Codespaces workflow

---

# Conclusion

Despite multiple local setup challenges on macOS Catalina, I successfully completed the Docker learning and deployment workflow using GitHub Codespaces.

This journey helped me understand:

* Docker basics
* Containerization workflow
* Image building and deployment
* Docker Compose
* Real-world troubleshooting approaches

The project was successfully completed and pushed to both GitHub and Docker Hub.
