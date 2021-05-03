## Installation of K8S on AWS using KOPS:

### We need a domain name which can be bought from `Godaddy`
- Domains > search > pick a domain > checkout

### We need to create a Route53 zone with the same domain name we bought
- AWS > Networking & Content Delivery > Select Route53
- Hosted zones > create Hosted zone > Copy the domain name from Godaddy and select `Public Hosted Zone` and create it
- You can see NS for the created hosted zone

### Configure godaddy domain to use the Route53 Name servers
- Godaddy > My Domains > DNS Settings > Add all the `Nameservers` created in the Route53 to Godaddy

### Deploy a EC2 Linux server on AWS and download tools KOPS & KUBECTL
- Before Deploying a EC2 Linux amd Server, check VPC, Subnets.
- Connect to EC2 server with the `ssh` and go to root with the command `sudo su -`
- To install KUBECTL follow the steps from the [Kubernetes.io]{https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/}
 - To give permission `chmod 700 kubectl`
- To install KOPS
 -Go to `KOPS download Github` > `Releases` > `Kops-linux-amd64` >right click `copy link location`
 -In Powershell `wget` `copy link location`, `ll` to check
 - To give permission `chmod 700 kubectl`
 - `echo $PATH` > `pwd` > `cd /etc/` > `cd ~` > `mv kubectl /usr/local/sbin/` > `mv kops-linux-amd64 /usr/local/sbin/`

### Create a S3 Bucket. The K8S config will be saved in this S3 Bucket.
- AWS > Storage > S3 > Create a bucket with the region

### Create a AWS Access Key and Secret Key and user must have W/R access to the S3 bucket.
- AWS > Security, Identity & Complaince > IAM > USERS > Add user > Add permissions > Select `AdminstratorAccess`just in this now(not advisable to give in all cases) > create access key > Save `Access key ID`, `Secret access key`
To configure AWS > In the Powershell > `aws configure` > give the access key ID, Secret access key, Default region > Default Output format (Json)

### create a ssh key pair by rinning `ssh-keygen` in root home folder

### To create Kops cluster 
- To create config
> kops create cluster --name=${domain-name} --state=s3://${S3-bucket-name} --zones=${xx-xxxx-xx} --node-count=2 --node-size=t3.medium --master-size=t3.medium --dns-zone=${domain-name}

- To update 
> kops update cluster ${domain-name} --yes --state=s3://${S3-bucket-name}

- Refresh the EC2- missions will start, Route53 - records will create
