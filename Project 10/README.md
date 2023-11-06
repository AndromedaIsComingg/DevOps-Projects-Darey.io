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


One the diagram below, you can seea common pattern where several stateless Web Servers share a common database and also access the same files using Network FIle System (NFS) as a shared storage file. Even though the NFS server might be located on a completely seperate hardware, for the Web Server, it looks like a local file system from where they can serve the same files.


<img width="741" alt="Screen Shot 2023-11-02 at 6 14 36 PM" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/c84a3d85-0a1a-4a22-8d4c-9c9cdaa653c8">




##### Create mount points on /mnt directory for logical volumes as follows:
Using the `mkdir` command, we will make the following directories and mount accordingly
- Mount lv-apps on /mnt/apps (to be used by webservers)
- Mount lv-logs on /mnt/logs (tp be used by webservers logs)
-  Mount lv-opt on /mnt/opt ( to be used bu jenkins server in the subsequent project)
  This is done using the commands:
`sudo mount /dev/webdata-vg/lv-apps /mnt/apps
sudo mount /dev/webdata-vg/lv-opt /mnt/pot
sudo mount /dev/webdata-vg/lv-logs /mnt/logs`

## Implementing a Business Website Using NFS for the Backend File Storage
We will begin by launching Linux RedHat EC2 instance, named "Web Server" 


## Install NFS server, configure it to start on reboot and make sure it is up and running
