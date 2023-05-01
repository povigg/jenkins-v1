# Installation

## Build the Jenkins-BlueOcean Docker Image

```
docker build -t myjenkins-blueocean .
```

## Create bridge network in Docker

```
docker network create jenkins
```

## Run the container
### On macOS and Linux

```
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean
  ```
  
  ### On Windows
  
  ```
  docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean
  ```
  
  ## Connect to Jenkins
  
  ```
  http://localhost:8080/
  ```
  
  ## Get Jenkins password
  
  ```
  docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
  ```
  
  ### Reference
(https://www.jenkins.io/doc/book/installing/docker/)

### Setup Docker on local machine as Jenkins agent
(https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin)

