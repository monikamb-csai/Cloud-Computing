## Experiment 1: Containerize and Run a Simple Python Web Application

### Objective

To learn how to create a simple Python web application, package it into a Docker image, run it as a Docker container, and access the application from a web browser.

### Technologies Used

- Python
- Flask
- Docker
- Docker Desktop
- PowerShell

### Files

- `app.py`
- `requirements.txt`
- `Dockerfile`

### Docker Image

`my-python-app`

### Docker Container

`my-python-container`

### Application Port

`5000`

### Application URL

`http://localhost:5000`

### Main Commands

```text
docker --version
docker run hello-world
docker build -t my-python-app .
docker images
docker run -d -p 5000:5000 --name my-python-container my-python-app
docker ps
docker logs my-python-container
docker stop my-python-container
docker start my-python-container
docker rm my-python-container
docker ps -a
