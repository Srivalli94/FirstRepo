DInd: Docker inside Docker:
1.	Check where the .pem file is located in the system and go that folder.
2.	Copy the ssh link from the EC2 server and paste it.
Ex: PS C:\Users\S.Tummalapalli\Downloads> ssh -i "amma.pem" ubuntu@ec2-18-193-76-75.eu-central-1.compute.amazonaws.com
3.	Check for docker with the command: docker version (Otherwise follow the steps from the docs.docker.com to install respective to your OS)
4.	Check for docker images if already Jenkins is running in it with the command: docker images.
5.	Otherwise, this time will try with Dockerfile.
6.	Go to the system’s home directory, check for Ubuntu. (As it is in the home dir., sudo not required, otherwise use sudo.) 
7.	Make a directory with the command: mkdir [folder name] &Change to that directory: cd [folder name]
8.	To create and edit the Docker file, will use a ‘vi editor’: vi Dockerfile, to edit it press, shift+i.
9.	With the command: FROM jenkins/Jenkins:latest, will download Jenkins latest from Jenkins images. To exit from the vi editor, click ESC and write command: :x
10.	To build Jenkins, create a tag to it with the command: docker build -t [tag_name].
11.	Check for docker images and run it.
12.	Check for all the containers with the command: docker ps -a
13.	With the command: sudo chmod 777 /var/run/docker.sock you will access to docker.sock.
14.	Now to run use the command: docker run -d  - -name [tag_name] -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock -v /usr/bin/docker:/usr/bin/docker [tag_name]
15.	Check for all the containers, docker ps -a
16.	To get the password for Jenkins us the command: docker logs [container_ID]

To run a pipeline script:
1.	Go to manage Jenkins>manage plugins>search for docker in available>add docker plugin, docker API, docker pipeline. Install without restart.
2.	Go to Manage Jenkins>mange nodes>configure clouds>Select Docker>test connection,
3.	Check it enable it and save.
4.	Newitem> pipeline> give any name> git hub project
5.	As we want to build a simple java maven app copy the git hub repository URL and paste it in the URL: https://github.com/jenkins-docs/simple-java-maven-app/
6.	Pipeline script:
pipeline {
 agent {
 docker {
 image 'maven:3-alpine'
 args '-v /root/.m2:/root/.m2'
 }
 }
 stages {
 stage('checkout') {
 steps {
 checkout([$class: 'GitSCM', branches: [[name: '*/main']],
doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [],
userRemoteConfigs: [[url: 'https://github.com/david1412/java-program.git']]])
 }
 }
 stage('Build') {
     steps {
 sh 'mvn -B -DskipTests clean package'
 }
 }
 stage('Test') {
 steps {
 sh 'mvn test'
 }
 post {
 always {
 junit 'target/surefire-reports/*.xml'
 }
 }
 }
 stage('Deliver') {
 steps {
 sh './jenkins/scripts/deliver.sh'
 }
 }
 }
}
7.	Click build now.
8.	 
9.	By clicking on each stage>logs we can see an overview of what is going on.
10.	By clicking on the Delivery stage>logs, we can see that the build is success and the code too. 
11.	In this, I have learnt how to write and build a project.


