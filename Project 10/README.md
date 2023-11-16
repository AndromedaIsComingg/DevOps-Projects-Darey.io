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


Export the mount for webservers' `subnet CIDR` to connect a clients. For simplicity, you will install your three Web Servers inside the same subnet, but in production set up you would probably want to seperate each tier inside its own subnet for higher level of security. To check your `subnet CIDR`, open your EC2 details in AWS web console and locate the "Networking tab and open a Subnet link, which will open a new window from where we will check the subnet and locate the `IPV4 CIDR` uder which the subnet CIDR appears as shown in the diagrams below.


<img width="1058" alt="subnet network" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/5d666aff-3481-40b4-98fd-7569f362b3bf">


<img width="1005" alt="subnet CIDR" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/48a2bb37-2ec8-41af-b581-b97ad932826c">


We will configure permission that will allow the Web Servers to read, write and execute files on NFS with the following command.
sudo chown -R nobody: /mnt/apps
sudo chown -R nobody: /mnt/logs
sudo chown -R nobody: /mnt/opt

`sudo chmod -R 777 /mnt/apps
sudo chmod -R 777 /mnt/logs
sudo chmod -R 777 /mnt/opt`

and restart NFS with the command below
`sudo systemctl restart nfs-server.service`


<img width="551" alt="ownership" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/552b3754-6686-402c-af40-a098f92ec235">


Configure access to NFS for clients within the same subnet (example of Subnet CIDR - 172.31.32.0/20)

This will be done by editing an `export` file with the vi text editor

sudo vi /etc/exports

/mnt/apps <Subnet-CIDR>(rw,sync,no_all_squash,no_root_squash)
/mnt/logs <Subnet-CIDR>(rw,sync,no_all_squash,no_root_squash)
/mnt/opt <Subnet-CIDR>(rw,sync,no_all_squash,no_root_squash)

<img width="446" alt="export" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/1bde40a8-cb5c-4f7c-87be-bc7cdfd8f12f">


Now it is time to check which port is used by NFS and open it in the Inbound rule of the Security Group.

That is done using the command `rpinfo -p | grep nfs`


<img width="370" alt="check port" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/434abbfb-ef23-4085-99bc-759100d5fe6f">


In order for NFS server to be accessible from your client, you must also open the following ports: TCP 111, UDP 111, UDP 2049.


<img width="1197" alt="inbound rules" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/9636ef22-afab-4da7-a6bc-62d4bdfe1927">

## Configuring a backend database as part of 3 tier architecture

##### Installing MySQL server
This is done with the command `sudo yum install mysql-server` 


<img width="714" alt="mysql server install" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/237510fb-980f-4f04-9c1e-a3ed83bbd361">


##### Create a Database 
We will create a Database and name it `tooling` and a User `webaccess` and grant permission to `webaccess` user on `tooling` database to do anything only from the webservers `subnetcidr` using the following command
`sudo mysql
CREATE DATABASE tooling;
CREATE USER `webaccess`@`172.31.16.0/20` IDENTIFIED BY 'mypass';
GRANT ALL ON tooling.* TO ‘webaccess’@‘172.31.16.0/20';
FLUSH PRIVILEGES;
SHOW DATABASES;
exit`


<img width="523" alt="Create DB   User" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/c6556dd3-359e-43de-9847-320d413cda66">



## Prepare the Web Servers
We need to make sure that our Web Servers can serve the same content from shared storage solutions, in our case - NFS Server and MySQL database. You already know that one DB can be accessed for reads and writes by multiple clients. For storing shared files that our Web Servers will use - we will utilize NFS and mount previously created Logical Volume `Lv-apps` to the folder where Apache stores files to be served to the users `(/var/www.)`.


This approach will make our Web Servers stateless , which means we will be able to add new ones or remove them whenever we need, and the integrity of the data (in the database and on NFS) will be preserved.
During the next steps we will do following:
• Configure NFS client (this step must be done on all three servers)
• Deploy a Tooling application to our Web Servers into a shared NFS folder
• Configure the Web Servers to work with a single MySQL database

##### Launch a new EC2 instance with RHEL 8 Operating System
![Screen Shot 2023-11-09 at 4 19 23 PM](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/5844a1db-963f-4cc9-aacd-99603157d04c)


##### Install NFS Client


The install the `NFS Client` with the command `sudo yum install nfs-utils nfs4-acl-tools -y`


<img width="654" alt="NFS client" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/c88bd0ca-1f52-4d48-a554-e3e1eabe4cf3">


##### Mount `/var/www/` and target the NFS server's export for app
This is done with the following command `sudo mount -t nfs -o rw,nosuid <NFS-Server-Private-IP-Address>:/mnt/apps /var/www`
