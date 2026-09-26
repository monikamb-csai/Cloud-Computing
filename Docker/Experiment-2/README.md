## Experiment 2: Run, Test and Manage a Docker Container

### Objective

To learn how to use an existing Docker image to create a container, check whether the container is running, test the application, view logs, inspect the container, enter the container, stop and restart it, and finally remove it.

### Technologies Used

- Docker
- Docker Desktop
- PowerShell
- Python
- Flask

### Docker Image

`my-python-app`

### Docker Container

`test-python-container`

### Application Port

`5001:5000`

### Application URL

`http://localhost:5001`

### Main Commands

```text
docker --version
docker images
docker run -d -p 5001:5000 --name test-python-container my-python-app
docker ps
Invoke-WebRequest http://localhost:5001
(Invoke-WebRequest http://localhost:5001).Content
docker logs test-python-container
docker inspect test-python-container
docker exec -it test-python-container /bin/sh
ls
pwd
exit
docker stop test-python-container
docker ps -a
docker start test-python-container
docker ps
docker rm test-python-container
docker images
