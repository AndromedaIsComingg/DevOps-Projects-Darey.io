# Devops Tooling Website Solution

This Project is aimed at exploring the integration of various tools and technologies to create a unified platform that enhances collaboration, automation, and efficiency for software development and operations teams.

These tools are well known and widely used by multiple DevOps teams, so we will introduce a single DevOps Tooling Solution that will consist of:

1. Jenkins - free and open source automation server used to build CI/CD pipelines.
2. Kubernetes - an open-source container-ochestration system for automating computer application deployment, scaling, and management.
3. Jfrog Artifactory - a Universal Repository Manager supporting all major packaging formats, build tools and CI servers
4. Rancher - an open-source software platform that enables organizations to run and manage Docker and Kubernetes in production.
5. Grafana - a multi-platform open-souce analytics and interactive visualization web application.
6. Prometheus - an open-source monitoring system with s dimension data model, flexible query language, efficient time series database and modern alerting approach.
7. Kibana - this is a free and open user interface that lets you visualize your Elasticsearch data and navigate the Elastic Stack.  

##### Reqiurements
For this project execution, the following components will be required.
1. Infrastructure - AWS
2. Webserver - Linux RedHat Enterprise
3. Database Sever - Ubuntu + MySQL
4. Storage Server - Linux RedHat Enterprise
5. Programming Language - PHP
6. Code Repository - GitHub
7. Stable network connection
8. Access to the terminal
9. A user account with sudo privileges
10. A Laptop or PC to serve as a client




##### Prerequisites
- Knowledge of how to create an EC2 Instance and how to connect to it. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/Other-Projects/blob/main/Project%204/README.md)
- Understanding of basic Unix command knowledge. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/Other-Projects/blob/main/Project%201-Linux_Pracice_Project/README.md)
- How to implement a website with LVM Storage Management. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/Other-Projects/blob/main/Project%209/README.md)


The difference in the LVM will be creating from the one above will be our mount point directory `/mnt`, Where `lv-apps` will be mounted on `/mnt/apps`, `lv-logs` will be mounted on `/mnt/logs` and `lv-opt` will be mounted on `/mnt/opt` 


<img width="526" alt="logical volumes" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/0e613661-177d-4fd5-a3cd-f6f9d9ae413a">


Also, instead of formating the disks as `ext4`. we will formats them as `xfs`

<img width="567" alt="xfs format" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/16c6bd85-6718-4869-8a71-6c674ec0adf9">


In the diagram below, you can see a common pattern where several stateless Web Servers share a common database and also access the same files using Network FIle System (NFS) as a shared storage file. Even though the NFS server might be located on a completely seperate hardware, for the Web Server, it looks like a local file system from where they can serve the same files.


<img width="741" alt="Screen Shot 2023-11-02 at 6 14 36 PM" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/c84a3d85-0a1a-4a22-8d4c-9c9cdaa653c8">



## Implementing a Business Website Using NFS for the Backend File Storage
We will begin by launching Linux RedHat EC2 instance, named "Web Server" 



##### Create mount points on /mnt directory for logical volumes as follows:
Using the `mkdir` command, we will make the following directories and mount accordingly
- Mount lv-apps on /mnt/apps (to be used by webservers)
- Mount lv-logs on /mnt/logs (tp be used by webservers logs)
-  Mount lv-opt on /mnt/opt ( to be used bu jenkins server in the subsequent project)
  This is done using the commands:
`sudo mount /dev/webdata-vg/lv-apps /mnt/apps`
'sudo mount /dev/webdata-vg/lv-opt /mnt/pot`
`sudo mount /dev/webdata-vg/lv-logs /mnt/logs`


<img width="585" alt="mount" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/8de33c88-d736-4e3f-b6ff-59eedba0d6c8">



Checking the logical volumes with the command `df -h`

<img width="607" alt="mount + df -h" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/82336484-2c6e-498c-82e5-d8f1de484009">


## Install NFS server, configure it to start on reboot and make sure it is up and running
We execute this using the command `sudo yum install nfs-utils -y`

<img width="676" alt="NFS utility instal" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3d3f7eba-d700-44bf-a667-b973cf4f9712">


Then we start the service, enable it and check the status with the commands below

`sudo systemctl start nfs-server.service`
`sudo systemctl enable nfs-server.service`
`sudo systemctl status nfs-server.service`


<img width="914" alt="NFS start enable   status" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/38ec6101-e72f-4c8c-9741-a2cd57e2d3f3">



