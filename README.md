# Basics of how to Launch instance in EC2, run and update jenkins
 
- Select free tier and `click Next: configure instance details`
- Check instance details and `click Next: Add Storage`
- Check Add storage and `click Next: Add tags`
- Add rule: selct `custom TCP rule`, Port range:8080 review and launch
- Select `choose an existing key pair` if you  already downloaded a key pair otherwise click “create new key pair”  then “ give a key pair name” and download key pair
- Check where the .pem file is in the system
- Open Windows Powershell
- Go to the folder in which the.pem file is installed.(Can also be done through Putty)
- In EC2, click on instance and `connect`.
- In the ssh client, copy ssh -i "xxx.pem" ubuntu@ec2-xx-xx-xxx-xxx.eu-xxxxxx-x.compute.amazonaws.com and paste it in the powershell

## Check “docker version”
To install docker in your selected instance, follow the steps in this link:[Install docker](https://docs.docker.com/engine/install/ubuntu/)
To Check whether docker is installed or not, its version and other details with the command:
> docker version

To pull jenkins with desired version
>docker pull jenkins/jenkins:`desired version`

Check for docker images
> docker images

Jenkins image can be seen in the images.

Run docker container in the port with image id
> docker container run -p 8080:8080 `container_id`

If the images Ids are unique, no need to write the whole Image ID just first few digits are enough.

A password is generated:xxxxxxxxxxxxxxxxxxxxx for logging into jenkins.

Now copy the Public IP address from the EC2 instance and then paste it in the URL with :8080 port 
Hopefully the Jenkins has to run in the system and it will ask for password. 
Copy the jenkins password and create username and fill other details and click save and continue.

## Update Jenkins to a higher version or or lower version:
Check all the containers:
>docker ps -a
 
If it is exited, we need to start to the container: 
> docker container start `container_id`
 
Execute the docker container: 
> docker container exec -u 0 -it `container_id` bash

Now we will enter into the container:
- To update it to an other version:
- Go to jenkins.io website. Click download, In stable LTS, click on past releases:
- Select whichever version to change: copy the URL and write the following command: wget and paste the link.
 
Restart container from the local host:
> docker conatiner restart `conatiner_id`
 
If we refresh the Jenkins we will go the desired version, In my case: 2.222.3 and it can be seen that manage jenkins page.

In this session we have learned how to spin Jenkins and update it.