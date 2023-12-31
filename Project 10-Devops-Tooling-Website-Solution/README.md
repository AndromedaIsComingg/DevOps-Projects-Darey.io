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


Export the mount for webservers' `subnet CIDR` to connect as clients. For simplicity, you will install your three Web Servers inside the same subnet, but in production set up you would probably want to seperate each tier inside its own subnet for higher level of security. To check your `subnet CIDR`, open your EC2 details in AWS web console and locate the "Networking" tab and open a Subnet link, which will open a new window from where we will check the subnet and locate the `IPV4 CIDR` uder which the subnet CIDR appears as shown in the diagrams below.


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
This where we will spin up another Linux instance which will be Ubuntu version 20.04

##### Installing MySQL server
This is done with the command `sudo yum install mysql-server` 


<img width="714" alt="mysql server install" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/237510fb-980f-4f04-9c1e-a3ed83bbd361">


##### Create a Database 
We will create a Database and name it `tooling` and a User `webaccess` and grant permission to `webaccess` user on `tooling` database to do anything only from the webservers `subnetcidr` using the following command
`sudo mysql
CREATE DATABASE tooling;
CREATE USER `webaccess`@`172.31.16.0/20` IDENTIFIED BY 'mypass';
GRANT ALL PRIVILEGES ON tooling.* TO `webaccess`@`172.31.16.0/20`;
FLUSH PRIVILEGES;
SHOW DATABASES;
exit`


GRANT ALL ON tooling.* TO ‘webaccess’@‘172.31.16.0/20';


<img width="523" alt="Create DB   User" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/c6556dd3-359e-43de-9847-320d413cda66">

We will also use a text editor to edit the following file `sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
where we will be changing the `bind-address` and `mysqlx-bind-address` to `0.0.0.0`
and restart `MySQL` using `sudo systemctl restart mysql`
<img width="709" alt="Bind address" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/472ce468-1449-427a-9c67-d45853900e34">




## Prepare the Web Servers
We need to make sure that our Web Servers can serve the same content from shared storage solutions, in our case - NFS Server and MySQL database. You already know that one DB can be accessed for reads and writes by multiple clients. For storing shared files that our Web Servers will use - we will utilize NFS and mount previously created Logical Volume `Lv-apps` to the folder where Apache stores files to be served to the users `(/var/www.)`.


This approach will make our Web Servers stateless , which means we will be able to add new ones or remove them whenever we need, and the integrity of the data (in the database and on NFS) will be preserved.
During the next steps we will do following:
• Configure NFS client (this step must be done on Web Servers)
• Deploy a Tooling application to our Web Servers into a shared NFS folder
• Configure the Web Servers to work with a single MySQL database

##### Launch a new EC2 instance with RHEL 8 Operating System 
This instance will be hosting one of our web servers

![Screen Shot 2023-11-09 at 4 19 23 PM](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/5844a1db-963f-4cc9-aacd-99603157d04c)


##### Install NFS Client

The install the `NFS Client` with the command `sudo yum install nfs-utils nfs4-acl-tools -y`


<img width="654" alt="NFS client" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/c88bd0ca-1f52-4d48-a554-e3e1eabe4cf3">


##### Mount `/var/www/` and target the NFS server's export for app
First we wil create the directory `sudo mkdir /var/www`
Then we will mount with the following command `sudo mount -t nfs -o rw,nosuid <NFS-Server-Private-IP-Address>:/mnt/apps /var/www`
verify that NFS was mounted successfully using the command `df -h`


<img width="443" alt="df -h serv1" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/458fba92-92a9-42f3-ba96-f08faae76929">


Also, we will make sure the changes persist on the web server after reboot by editing the following file `sudo vi /etc/fstab` and adding the following line of code `<NFS-Server-Private-IP-Address>:/mnt/apps /var/www nfs defaults 0 0`


<img width="770" alt="vi fstab edit" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/310c074d-4abb-4e25-a022-b9de2d200fc6">


##### Installing Apache
This is done so that content can be served to the end user, it is done using the command `sudo yum install httpd -y`

<img width="648" alt="install httpd" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/861e4875-cfbd-4030-b8d6-0c406557895e">


We will repeat the same step in creating another web server and mount it accordingly.
We will verify that Apaches files and directory are available on the Web Server `/var/www` and also confirm that same file appear on `/mnt/apps` directory of the `NFS` Server. 
We can solidify this test further by creating a new file from one server and see if the file is accessible from the other Web Server and the NFS sever. For example, lets create a file called `test.txt` on `/var/www` and confirm it on `mnt/apps` 

<img width="444" alt="touch txt" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/8daf483e-472b-4b95-8426-52f12eb9f829">

Confirmning from the `NFS` Server side

<img width="337" alt="touch confirmd" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/fd9cb41a-6a07-4d71-a9db-b5a20bbe00c9">


The log folder of Apache on the Web Server `/var/log/httpd` is going to be mounted on NFS Server's export logs `/mnt/logs`. 
This will be done with the command `sudo mount -t nfs -o rw,nosuid <NFS-Server-Private-IP-Address>:/mnt/logs /var/log/httpd`

<img width="723" alt="mount log   fstab" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/91d2948f-5392-412a-bf2d-4a22f8061211">

Afer which we will make sure that the mount persists after reboot by editing again the file `/etc/fstab` and adding `<NFS-Server-Private-IP-Address>:/mnt/logs /var/log/httpd nfs defaults 0 0`

<img width="663" alt="fstab 2" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/528fb69d-565f-4cbf-b6c9-b5d9e17de480">

##### Forking Tooling Source Code
We are going to fork a source code from a Github Account into your Github account
We will begin this by intsalling git on the Web Server with the comand `sudo yum install git`  after which we will intialize git with the command `git init` 

<img width="606" alt="git init" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/8dce7a67-d919-43b2-8289-f6385cb746ec">


then clone the repo by copying the `HTTPS` URL code from the repo 

<img width="948" alt="Darey repo" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/86017ffc-f5ed-458a-8d57-e3f65da0a660">


and running the command `git clone <HTTPS URL>` and we will confirm this with the `ls` command

<img width="610" alt="git clone + ls" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/a061ee9f-9435-4117-b63b-486f0564a06c">


We will proceed to copy the folder `html` which is a sub directory in the `tooling` folder to `/var/www/html`
using the command `sudo cp -R html/. /var/www/html` while we already changed directory into the `tooling` folder

<img width="651" alt="copy tooling" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3c5a790f-76df-406b-adce-caca7a490bf0">

please note that `port 80` has to be open on the web server's security group to allow http connections.


Now we can test the configuration by launching the public IP of the Web Server in a Web Browser
<img width="1228" alt="test page" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/0f3d1295-9799-4f4a-915c-3fe64f504cdf">


If we do not get a page similar to one above, you may need to check permissions to /var/www/html folder and also disable SELinux sudo setenforce 0

To make this change permanent, we will open the file `sudo vi etc/sysconfig/selinux and set SELINUX-disabled`

##### Update the website's configuration to connect to the database (in function.php file). Apply tooling-db.sql script
This will be done by editing the file `sudo vi /var/www/html/functions.php`

<img width="583" alt="function PHP" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/9a20981d-ee7e-4be3-9439-3fa9acab4341">


##### Create in MySQL a new user with username: myuser and pasword: password
To carry this out, we need to first install MySQL Client with the command `sudo yum install mysql`
followed by `mysql -h <PRIVATE-IP-OF-DATABASE> -u webaccess -p tooling < tooling-db.sql` which should throw no error.

please note that the inbound rule for the Database server has to be set to open to MYSQL/AURORA with the subnet/CIDR of the Web Server


<img width="1222" alt="DB inbound" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/89023efa-d8ff-4e3e-83ce-c9b2bc727888">

Renaming the Default Hompage File
This is done so that the customized tooling page can prevail. It is done from the path `/etc/httpd/conf.d/welcome.conf`


using the command `sudo mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.backup` after which we will restart `Apache` with the command `sudo systemctl restart httpd`


<img width="770" alt="rename   restart httpd" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3be0fdc7-50c9-46f0-887d-a19c229bbc35">


`show databases;
use tooling;
show tables;
select * from users;`


<img width="637" alt="TAbles" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/18facaa9-65f6-47bf-90e9-9b340f62b8ee">


We will now log in with the credentials Username Admin and Password Admin from the web browser
'http://Web-Server-Public-IP-Address-or-Public-DNS-Name/index.php'

![home log in](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/7d8a9d1b-55f8-4671-8958-09c1a82b145e)


![home page](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/c74354af-f01e-4bde-8dcf-26d9f357f2ef)


---------------------------------![Alt Text](https://cssbud.com/wp-content/uploads/2021/05/thanks-for-your-time.gif)---------------------------------------------



