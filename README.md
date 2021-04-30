# Dind: Docker inside Docker:
Check where the .pem file is located in the system and go that folder.Copy the ssh link from the EC2 server and paste it.

Check for docker with the command `docker version` (Otherwise follow the steps from the [docker website](https://docs.docker.com/engine/install/ubuntu/) to install respective to your OS)

Check for docker images if already Jenkins is running in it with the command `docker images`. Otherwise, this time will try with Dockerfile.

Go to the system’s home directory, check for Ubuntu. (As it is in the home dir., sudo not required, otherwise use sudo.) 

Create a directory with the command: mkdir [folder name] &Change to that directory: cd [folder name]

To create and edit the Docker file, will use a ‘vi editor’: vi Dockerfile, to edit it press, shift+i. Check the Dockerfile.txt  

To exit from the vi editor, click `ESC` and write command: `:x`

To build Jenkins, create a tag to it with the command `docker build -t [tag_name] .` 

Check for docker images and run it.


With the command: `sudo chmod 777 /var/run/docker.sock you will access to docker.sock`.

Now to run use the command: `docker run -d  - -name [container_name] -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock -v /usr/bin/docker:/usr/bin/docker [tag_name]
`
Check for all the containers, docker ps -a

To get the password for Jenkins us the command: `docker logs [container_ID]
`
## To run a pipeline script:
Go to manage Jenkins>manage plugins>search for docker in available>add docker plugin, docker API, docker pipeline. Install without restart.

Go to Manage Jenkins>mange nodes>configure clouds>Select Docker>test connection,

Check it enable it and save.

Newitem> pipeline> give any name> git hub project.

As we want to build a simple java maven app copy the git hub repository URL and paste it in the URL: https://github.com/jenkins-docs/simple-java-maven-app/
Pipeline script: 

Click build now.
 
By clicking on each stage>logs we can see an overview of what is going on.

By clicking on the Delivery stage>logs, we can see that the build is success and the code too. 

In this, I have learnt how to write and build a project.


