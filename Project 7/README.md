# Implementing Loadbalancers with Nginx

#### What is load balancing?
Load balancing is the method of distributing network traffic equally across a pool of resources that support an application. Modern applications must process millions of users simultaneously and return the correct text, videos, images, and other data to each user in a fast and reliable manner. To handle such high volumes of traffic, most applications have many resource servers with duplicate data between them. A load balancer is a device that sits between the user and the server group and acts as an invisible facilitator, ensuring that all resource servers are used equally.

##### The concept is shown by the illustration below

<img width="861" alt="Introduction Image" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/8a6ea022-db0f-4241-9a09-48e45f816620">



Nginx is a versertile software, it can act like a web server, reverse proxy, and a load balancer. All that is needed is to configure it properly for which purpose.

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

###### 1. Create and Configure two linux based server using the AWS EC2 console

Instance A name - `Apache Server`


Instance B name - `Nginx Loadbalancer`

<img width="1280" alt="EC2 Spinning" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/80e76f5b-56b7-4f7b-8875-969e4250752c">


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
For Instance A, the Sever, we will be opening port 8000 and port 80 will be openned for Instance B, the Load balancer. This will be done by creating a new entry in the "inbound rules" in the Instances' security group.
Instance a will also be configured to allow traffic from anywhere.

##### Below we add the inbound rule 8000 to Instance A
<img width="1278" alt="Inbound Apache server" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/7e16292b-7b2b-449b-9f1f-7f2a59af28c4">


##### Below we add the inbound rule 80 to Instance B
<img width="1262" alt="Inbound Nginx Loadbalancer" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/d234b132-0216-40b2-a934-dbb3693cd887">


## Connecting to the EC2 Instances
###### Connect to the EC2 instance by running the command `ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>`
This connects terminal to the EC2 instance using SSH, which is a Secure Shell network communication protocol that enables two computers to communicate.

<img width="567" alt="terminal apache server" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/3fac61ed-291d-49f8-b9ee-40ab2aed4472">


##### Next we will install Apache using the command below
`sudo apt update -y &&  sudo apt install apache2 -y`
##### it is important to note that :
- the `sudo apt update` side of the command is to update the server
- the && (Ampersand and) is a module to combine two commands
- the `-y` in the command is to answer yes to future yes/no prompts when the command is running.

<img width="553" alt="Apt update + apache instl" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/e260f65b-cbdb-4a05-ba65-9e838261d32a">


##### Now we will verify that apaches is running using the folowing command
`sudo systemctl status apache2`

<img width="669" alt="Status Apache" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/e4c96429-9e0f-4da5-970a-1795b3ab3b74">


##### Configure Apache to serve a page showing its public ip
we will start this by configuring Apache webserver to serve content on port 8000 instead of the default port 80, then we will create an index.html file which will be configured to display thre publice ip of the EC2 instance, then we will override the Apach webserver's default html file.


##### Configuring Apache to serve content on port 8000
Using a prefered text editor such as nano, vi, vim etc, we will be editing a configuration file in the following path
`sudo vi /etc/apache2/ports.conf`


<img width="440" alt="conf port 8000" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/74f5e986-6bb4-4d3f-bac8-77a48f230258">


Using the vi editor, we now going to switch to insert mode by pressing key `i` and then adding a listen directive of 8000, afterwhich we will save and exit the vi editor with the comand `wq!` as shown below.


<img width="574" alt="vi listen 8000" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/35f3104d-4dff-48fb-8b1d-fd669a497427">


Still using the vi editor, we are now going to edit another configuration file in the path below. We are going to change port 80 to 8000.

`sudo vi /etc/apache2/sites-available/000-default.conf`


<img width="582" alt="conf 2  default" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/a9f1075c-5aaf-42f7-a854-c2d745d7d029">


Using the vi editor, we now going to switch to insert mode by pressing key `i` and then edit port 80 to 8000, afterwhich we will save and exit the vi editor with the comand `wq!` as shown below.


<img width="605" alt="vi conf dedualf edit" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/e67f8a15-2c1f-4ac6-b468-a5974ced2807">


##### Now we will have to restart Apache to load the new configuration using the following command
`sudo systemctl restart apache2`


<img width="409" alt="Apache restart" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/423b53c3-0881-4c14-b904-808275853507">


## Creating our new html file
Open a new index.html file with the following command
`sudo vi index.html`
<img width="324" alt="sudo indx html" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/f00bda96-bae1-4bf8-9578-7748f79491bf">


Now using the vi editor we are going to paste the following code inside the created html file as text and substitute the public ip in the place holder in the code and exit using `wq!`

``` html
<!DOCTYPE html>
        <html>
        <head>
            <title>My EC2 Instance</title>
        </head>
        <body>
            <h1>16.16.27.184</h1>
            <p>Public IP: YOUR_PUBLIC_IP</p>
        </body>
        </html>
```

<img width="330" alt="vi index html" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/ac9638b6-6d5d-437a-bc4c-4846927856e6">


##### Changing Ownership
Now we will change the ownership of the created file using the following command
`sudo chown www-data:www-data ./index.html`


<img width="496" alt="Change ownershp" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/5f02863e-b065-43f3-aa8e-f5b83bf29664">



