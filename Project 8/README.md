# Automating Loadbalancer configuration with Shell scripting



#### What is load balancing?
Load balancing is the method of distributing network traffic equally across a pool of resources that support an application. Modern applications must process millions of users simultaneously and return the correct text, videos, images, and other data to each user in a fast and reliable manner. To handle such high volumes of traffic, most applications have many resource servers with duplicate data between them. A load balancer is a device that sits between the user and the server group and acts as an invisible facilitator, ensuring that all resource servers are used equally.

##### The concept is shown by the illustration below

<img width="861" alt="Introduction Image" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/8a6ea022-db0f-4241-9a09-48e45f816620">



Nginx is a versertile software, it can act like a web server, reverse proxy, and a load balancer. All that is needed is to configure it properly for which purpose it is to be used for.

##### The concept of using Nginx as a load balancer is shown by the illustration below


![nginx-as-load-balancer](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/a296006e-1fd8-477b-9c6b-d281565f57cd)


#### The prerequisites for the implementation of Loadbalancers with Nginx on Linux are as follows:

- Stable network connection
- How to create an EC2 Instance
- Basic Unix command knowledge
- A system running Linux or an AWS EC2 instance running a Linux OS
- Access to the terminal
- A user account with sudo privileges

## AWS Account & EC2 Instance
###### Creating an AWS Account and spinning an EC2 instance.
From the AWS web platform `AWS.Amazom.com` we will sign up and create an account, after which we will check for EC2 in the compute services.
## Setting up a Basic Load Balancer

###### 1. Create and Configure three linux based servers using the AWS EC2 console
Two of which will be Apache Web servers and the third will be used to configure Nginx as a load balancer.

Instance A name - `Apache Server`


Instance B name - `Nginx Loadbalancer`


Instace C name - `Apache Server 2`


<img width="1280" alt="two instances" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/408c0749-2f1e-4de8-9ac4-1a7d0e6d35e8">



## Creating a private Key
###### Create and download a private key from the console
The private key created here was named `1stkey`

###### The .pem file was saved in the "Downloads" folder as shown below

<img width="320" alt="pem file in dwnlds" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/d73e3fac-39ac-42ef-a5d3-844018d53cbe">

###### From Terminal, working directory should be changed to the "Downloads" folder

This is done to direct terminal to recognize the generated key file from the directory where it was saved.
<img width="272" alt="cd Downloads" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/f0d64650-0ac8-40d6-b2ae-5177940e2a91">

###### From Terminal, permission should be changed for the private key.

This is done to grant access to the key file using the command `sudo chmod 0400 1stkey.pem`

Please note that that file extension must be added to the name of the key file.

<img width="412" alt="changing permission for private key" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/6890a6f6-da94-49d0-a2e5-cc5894f8888d">


###### 2. Creating Inbound Rules
For Instance A and C, the Servers, we will be opening port 8000 and port 80 will be openned for Instance B, the Load balancer. This will be done by creating a new entry in the "inbound rules" in the Instances' security group.
Instance a will also be configured to allow traffic from anywhere.

##### As below, we will add the inbound rule 8000 to Instance A (same will be carried out for instance C)
<img width="1278" alt="Inbound Apache server" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/7e16292b-7b2b-449b-9f1f-7f2a59af28c4">


##### Below we add the inbound rule 80 to Instance B
<img width="1262" alt="Inbound Nginx Loadbalancer" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/d234b132-0216-40b2-a934-dbb3693cd887">


## Connecting to the EC2 Instances
###### Connect to the EC2 instance by running the command `ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>`
This connects terminal to the EC2 instance using SSH, which is a Secure Shell network communication protocol that enables two computers to communicate.

<img width="567" alt="terminal apache server" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/3fac61ed-291d-49f8-b9ee-40ab2aed4472">


## Updating Index Files
##### It is best practice to update index files on the instance
This is done using the command `sudo apt update`, this downloads the most recent packages from sources.

<img width="815" alt="Apt update" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/958d18be-3629-490c-b014-53e2bf6c13e4">




## Deploying and Configuring the Webservers (Using shell scripting)
###### All the process we need to deploy our web server has been codified in the shell script below:
- This Automates the installation and configuration of Apache Webserver to listen on port 8000
- Usage : Call the script and pass in the public IP of your EC2 instance as the first argument as shown below
  `./install.sh <public IP>`


```bash
  #!/bin/bash

####################################################################################################################
##### This automates the installation and configuring of apache webserver to listen on port 8000
##### Usage: Call the script and pass in the Public_IP of your EC2 instance as the first argument as shown below:
######## ./install.sh <public IP>
####################################################################################################################

set -x # debug mode
set -e # exit the script if there is an error
set -o pipefail # exit the script when there is a pipe failure

PUBLIC_IP=$1

[ -z "${PUBLIC_IP}" ] && echo "Please pass the public IP of your EC2 instance as an argument to the script" && exit 1

sudo apt update -y &&  sudo apt install apache2 -y

sudo systemctl status apache2

if [[ $? -eq 0 ]]; then
    sudo chmod 777 /etc/apache2/ports.conf
    echo "Listen 8000" >> /etc/apache2/ports.conf
    sudo chmod 777 -R /etc/apache2/

    sudo sed -i 's/<VirtualHost \*:80>/<VirtualHost *:8000>/' /etc/apache2/sites-available/000-default.conf

fi
sudo chmod 777 -R /var/www/
echo "<!DOCTYPE html>
        <html>
        <head>
            <title>My EC2 Instance</title>
        </head>
        <body>
            <h1>Welcome to my EC2 instance</h1>
            <p>Public IP: "${PUBLIC_IP}"</p>
        </body>
        </html>" > /var/www/html/index.html

sudo systemctl restart apache2

```

## Creating a Shell script file to Install Apache
##### Now we will create a shell script file named `install` with as bash extension `.sh`, hence the file name will be `install.sh` 
This will be done with the vi text editor, on the vi text editor we will enter the insert mode with `i`, then we will paste the above script in it, press the `esc` key to leave the vi editor, afterwhich we will exit vi editor 
 with the command pressing `:` and typing `wq!` then  hit `enter`


<img width="824" alt="vi script apache" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/cc19dcc0-702c-4b1f-b9aa-f878575bb3a4">


 ##### Granting Permissions
 Now we will change the permissions on the file to make it executable with the following command `sudo chmod +x install.sh`

 
##### Running the Script
To run the created script, we can do so by adding `bash` or `./` in front of the file name (extension inclusive) followed by a space and the the public IP as shown below.

`bash install.sh <public IP` or `./install.sh <public IP>`


<img width="767" alt="Apache install" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/03be5509-7276-4896-8255-170427131e9e">


##### We will therefore repeat this process for the second Apache Instance, `Apache Server 2` so that we can have both instances running as an Apache server.


## Deployment of Nginx as a Load Balancer using Shell Script
##### Automate the Deployment of Nginx as a Load Balancer using Shell Script
Having successfully deployed and configured two webservers, we will move on to the load balancer which is `Instance B`


Now we will create a shell script file named `nginx` with as bash extension `.sh`, hence the file name will be `nginx.sh` 
This will be done with the vi text editor, on the vi text editor we will enter the insert mode with `i`, then we will paste the above script in it, press the `esc` key to leave the vi editor, afterwhich we will exit vi editor 
 with the command pressing `:` and typing `wq!` then  hit `enter`


```bash
#!/bin/bash

######################################################################################################################
##### This automates the configuration of Nginx to act as a load balancer
##### Usage: The script is called with 3 command line arguments. The public IP of the EC2 instance where Nginx is installed
##### the webserver urls for which the load balancer distributes traffic. An example of how to call the script is shown below:
##### ./nginx.sh PUBLIC_IP Webserver-1 Webserver-2
#####  ./nginx.sh <public IP Instance A>:8000  <public IP Instance C>:8000
############################################################################################################# 

PUBLIC_IP=$1
firstWebserver=$2
secondWebserver=$3

[ -z "${PUBLIC_IP}" ] && echo "Please pass the Public IP of your EC2 instance as the argument to the script" && exit 1

[ -z "${firstWebserver}" ] && echo "Please pass the Public IP together with its port number in this format: 127.0.0.1:8000 as the second argument to the script" && exit 1

[ -z "${secondWebserver}" ] && echo "Please pass the Public IP together with its port number in this format: 127.0.0.1:8000 as the third argument to the script" && exit 1

set -x # debug mode
set -e # exit the script if there is an error
set -o pipefail # exit the script when there is a pipe failure


sudo apt update -y && sudo apt install nginx -y
sudo systemctl status nginx

if [[ $? -eq 0 ]]; then
    sudo touch /etc/nginx/conf.d/loadbalancer.conf

    sudo chmod 777 /etc/nginx/conf.d/loadbalancer.conf
    sudo chmod 777 -R /etc/nginx/

    
    echo " upstream backend_servers {

            # your are to replace the public IP and Port to that of your webservers
            server  "${firstWebserver}"; # public IP and port for webserser 1
            server "${secondWebserver}"; # public IP and port for webserver 2

            }

           server {
            listen 80;
            server_name "${PUBLIC_IP}";

            location / {
                proxy_pass http://backend_servers;   
            }
    } " > /etc/nginx/conf.d/loadbalancer.conf
fi

sudo nginx -t

sudo systemctl restart nginx
```



 ##### Granting Permissions
 Now we will change the permissions on the file to make it executable with the following command `sudo chmod +x install.sh`

 
##### Running the Script
To run the created script, we can do so by adding `bash` or `./` in front of the file name (extension inclusive) followed by a space and the the public IP as shown below.

`bash install.sh <public IP` or `./install.sh <public IP>`


<img width="767" alt="Apache install" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/03be5509-7276-4896-8255-170427131e9e">
