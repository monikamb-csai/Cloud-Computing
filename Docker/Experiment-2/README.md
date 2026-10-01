# Experiment 2: Run, Test and Manage a Docker Container

## Objective

To use the existing Docker image `my-python-app` to create a container, check whether the container is running, test the application, view logs, inspect the container, enter the container, stop and restart it, and finally remove it.

## 1. Configuration

### Software and Tools

- Docker Desktop
- Docker
- PowerShell
- Windows 11
- Existing Docker Image `my-python-app`

### Existing Docker Image

The Docker image created in Experiment 1 was used:

`my-python-app:latest`

The image was not rebuilt in this experiment.

### Container Details

- Container Name: `test-python-container`
- Host Port: `5001`
- Container Port: `5000`
- Application: Flask
- Application URL: `http://localhost:5001`

## 2. Architecture

```text
                 Student Computer
                        |
                        v
             Existing Docker Image
                my-python-app
                        |
                        | docker run
                        v
             Docker Container
          test-python-container
                        |
                        | -p 5001:5000
                        v
              Flask Application
                Port 5000
                        |
                        v
              Windows Port 5001
                        |
                        v
             http://localhost:5001

                        |
                        v
                  Browser

```


## 3. Execution

docker --version

docker images

docker run -d -p 5001:5000 --name test-python-container my-python-app

docker ps

-->Test the Application

Open the browser and enter:

http://localhost:5001

Expected result:

Hello! My first Docker application is running.

Invoke-WebRequest http://localhost:5001

docker logs test-python-container

docker inspect test-python-container

docker exec -it test-python-container /bin/sh

docker stop test-python-container

docker start test-python-container

docker stop test-python-container

docker rm test-python-container

docker ps -a

docker images

## 4. Results

4.1 Docker Desktop

4.2 Docker Version

4.3 Existing Docker Image

4.4 Container Created and Running

4.5 Application Running on localhost:5001

4.6 PowerShell Application Test

4.7 Container Logs

4.8 Container Inspection

4.9 Entering the Container

4.10 Files Inside the Container

4.11 Container Stopped

4.12 Container Started Again

4.13 Container Removed

4.14 Docker Image Still Available
   
## 5. Conclusion

The existing Docker image my-python-app was successfully used to create and run the container test-python-container.

The application was tested using the browser and PowerShell. The container was successfully inspected, entered, stopped, restarted, and removed.

The Docker image remained available even after the container was removed.

## 6. Author

Monika.M.Bhandari

