# Experiment 1: Containerize and Run a Simple Python Web Application

## Objective

To create a simple Python Flask web application, build a Docker image from the application files, run the image as a Docker container, test the application using a web browser, view container logs, stop and restart the container, and finally remove the container.

## 1. Configuration

### Software and Tools

* Docker Desktop
* Docker
* PowerShell
* Visual Studio Code
* Windows 11
* Python
* Flask

### Project Files

The following files were created:

* `app.py`
* `requirements.txt`
* `Dockerfile`

### Docker Image

The Docker image created in this experiment:

`my-python-app:latest`

### Container Details

* Container Name: `my-python-container`
* Host Port: `5000`
* Container Port: `5000`
* Application: Flask
* Application URL: `http://localhost:5000`

---

## 2. Architecture

```text
                 Student Computer
                        |
                        v
                  app.py
                        |
                        v
                 Dockerfile
                        |
                        | docker build
                        v
             Docker Image
              my-python-app
                        |
                        | docker run
                        v
             Docker Container
             my-python-container
                        |
                        | -p 5000:5000
                        v
              Flask Application
                 Port 5000
                        |
                        v
              Windows Port 5000
                        |
                        v
          http://localhost:5000
                        |
                        v
                    Browser
```

---

## 3. Execution

### Step 1 — Check Docker Installation

```powershell
docker --version
```

### Step 2 — Test Docker

```powershell
docker run hello-world
```

### Step 3 — Create Project Folder

```powershell
cd Desktop
mkdir docker-python-app
cd docker-python-app
```

### Step 4 — Create `app.py`

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello! My first Docker application is running."

app.run(host="0.0.0.0", port=5000)
```

### Step 5 — Create `requirements.txt`

```text
flask
```

### Step 6 — Create `Dockerfile`

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY app.py .

EXPOSE 5000

CMD ["python", "app.py"]
```

### Step 7 — Check Project Files

```powershell
cd "$HOME\Desktop\docker-python-app"
dir
```

Expected files:

```text
Dockerfile
app.py
requirements.txt
```

### Step 8 — Build the Docker Image

```powershell
docker build -t my-python-app .
```

### Step 9 — Check the Docker Image

```powershell
docker images
```

Expected result:

```text
REPOSITORY       TAG       IMAGE ID       SIZE
my-python-app    latest    xxxxxxxx       xxxMB
```

### Step 10 — Create and Run the Container

```powershell
docker run -d -p 5000:5000 --name my-python-container my-python-app
```

### Step 11 — Check the Running Container

```powershell
docker ps
```

Expected result:

```text
CONTAINER ID   IMAGE          PORTS
xxxxxxxx       my-python-app  0.0.0.0:5000->5000/tcp
```

### → Test the Application

Open the browser and enter:

```text
http://localhost:5000
```

Expected result:

```text
Hello! My first Docker application is running.
```

### Step 12 — View Container Logs

```powershell
docker logs my-python-container
```

### Step 13 — Stop the Container

```powershell
docker stop my-python-container
```

Check the containers:

```powershell
docker ps
```

### Step 14 — Start the Same Container Again

```powershell
docker start my-python-container
```

Check the container:

```powershell
docker ps
```

Open the browser again:

```text
http://localhost:5000
```

### Step 15 — Remove the Container

```powershell
docker stop my-python-container
docker rm my-python-container
```

Check all containers:

```powershell
docker ps -a
```

### Step 16 — Check the Docker Image

```powershell
docker images
```

The image `my-python-app:latest` should still be available.

---

## 4. Results

### 4.1 Docker Version

Docker installation was successfully verified using `docker --version`.

### 4.2 Docker Hello World

The Docker installation was tested successfully using the `hello-world` image.

### 4.3 Project Folder

The `docker-python-app` project folder was successfully created.

### 4.4 Python Application

The Flask application was successfully created using `app.py`.

### 4.5 Requirements File

The required Flask package was specified in `requirements.txt`.

### 4.6 Dockerfile

The Dockerfile was successfully created with Python 3.12, Flask installation, port 5000, and the application startup command.

### 4.7 Docker Image Created

The Docker image `my-python-app:latest` was successfully built.

### 4.8 Container Created and Running

The container `my-python-container` was successfully created and started.

### 4.9 Application Running on localhost:5000

The Flask application was successfully accessed through:

`http://localhost:5000`

### 4.10 Container Logs

The application logs were successfully displayed using `docker logs`.

### 4.11 Container Stopped

The running container was successfully stopped.

### 4.12 Container Started Again

The same stopped container was successfully started again.

### 4.13 Container Removed

The container was successfully removed using `docker rm`.

### 4.14 Docker Image Still Available

The Docker image `my-python-app:latest` remained available even after the container was removed.

---

## 5. Conclusion

The Python Flask application was successfully containerized using Docker.

The Docker image `my-python-app` was created from the application files and Dockerfile. The image was used to create and run the container `my-python-container`.

The application was successfully tested through the browser using `http://localhost:5000`. The container was also checked, logged, stopped, restarted, and removed successfully.

The Docker image remained available after removing the container, demonstrating the difference between a Docker image and a Docker container.

---

## 6. Author

Monika
