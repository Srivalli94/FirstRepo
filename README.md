## Jcac-jenkins
- Spinup jenkins using JCasC
- Run sample java project to build and test running

## Prerequisites
- AWS > EC2 > Docker installation > Based on your OS image

## How to build
For building docker base images we should build it manually:
>docker build -t base_image/image-directory:version .

## Check for updates
`vi Dockerfile` check for the jenkins version. `vi plugins.txt` check for all the updated plugins

## Docker daemon permission
> sudo chmod 777 /var/run/docker.sock

## How to use infrastructure image
Command:
> docker run -d --name {container-name} -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock -v /usr/bin/docker:/usr/bin/docker base_image/image-directory_version

where `container-name` is a userdefined container name 

check for all the containers: `docker ps -a` and get the admin password `docker logs {container-name}`

## Build a java-sample project
- New > jobname > select pipeline > save
- Select > job nmae > go to pipeline copy the Sample-java project jenkinsfile from the `Jenkinsfile` and paste it in the pipeline script
- Apply> Save
- Build now