# vue-app-jenkins

## Build the Jenkins Blue Ocean Docker Image 

> docker build -t myjenkins-blueocean:2.462.3-1 .


## Create the network called jenkins

> docker network create jenkins

If you get this error

> Error response from daemon: network with name jenkins already exists

Just use this command to be sure it is there 

> docker network ls


## Start the container

> docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.462.3-1

## Get the password

> docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword



