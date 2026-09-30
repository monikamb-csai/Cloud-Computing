# Experiment 3: Push a Docker Image to Docker Hub 
 
## Objective 
 
To take the existing Docker image `my-python-app` created in Experiment 1, authenticate with Docker Hub, tag the image with a Docker Hub repository name, push the image to Docker Hub, and verify that the image is available in the online registry. 
 
## 1. Configuration 
 
### Software and Tools 
 
- Docker Desktop 
- Docker 
- PowerShell 
- Docker Hub 
- Windows 11 
- Internet Connection 
 
### Existing Docker Image 
 
The existing Docker image created in Experiment 1 was used: 
 
`my-python-app:latest` 
 
The image was not rebuilt in this experiment. 
 
### Docker Hub Details 
 
- Docker Hub Username: `monika035` 
- Repository Name: `my-python-app` 
- Image Tag: `v1` 
- Final Image Name: `monika035/my-python-app:v1` 
 
## 2. Architecture 
 
```text 
                 Student Computer 
                        | 
                        v 
             Existing Docker Image 
              my-python-app:latest 
                        | 
                        | docker login 
                        v 
               Docker Hub Login 
                        | 
                        | docker tag 
                        v 
            monika035/my-python-app:v1 
                        | 
                        | docker push 
                        v 
                   Docker Hub 
                        | 
                        v 
             my-python-app:v1

```
## 3.Exection

docker --version

docker images

docker login

docker tag my-python-app monika035/my-python-app:v1

docker images

docker push monika035/my-python-app:v1

## 4. Results

4.1 Docker Desktop

4.2 Existing Docker Image

4.3 Docker Hub Login

4.4 Image Tagged

4.5 Docker Image Push

4.6 Docker Hub Repository

4.7 Docker Hub v1 Tag

## 5. Conclusion

The existing Docker image my-python-app:latest was successfully tagged and pushed to Docker Hub as monika035/my-python-app:v1.

The Docker Hub repository and v1 tag were successfully verified.

## Author

Monika


