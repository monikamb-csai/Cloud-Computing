## 🐳 Docker

This project is containerized using **Docker** to provide a consistent and isolated environment for running the application.

### Docker Setup

1. Build the Docker image:

```bash
docker build -t my-project .
```

2. Run the Docker container:

```bash
docker run my-project
```

3. To view running containers:

```bash
docker ps
```

### Docker Files

* `Dockerfile` – Contains instructions to build the Docker image.
* `.dockerignore` – Specifies files and folders that should not be copied into the Docker image.

Using Docker makes it easier to run the project on different systems without manually installing all the required dependencies.
