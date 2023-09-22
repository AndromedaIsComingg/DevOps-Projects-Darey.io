# Understanding Client server Architecture with MYSQL as RDBMS

#### A client-server architecture refers to a system that hosts, delivers, and manages most of the resources and services that the client requests. In this model, all requests and services are delivered over a network, and it is also referred to as the networking computing model or client server network.

#### While a relational database management system (RDBMS) is a collection of programs and capabilities that enable IT teams and others to create, update, administer and otherwise interact with a relational database. RDBMSes store data in the form of tables, with most commercial relational database management systems using Structured Query Language (SQL) to access the database. However, since SQL was invented after the initial development of the relational model, it is not necessary for RDBMS use.

## The prerequisites for the installation of MySQL on Linux are as follows:

- Stable network connection
- A system running Linux or an AWS EC2 instance running a Linux OS
- Access to the terminal
- A user account with sudo privileges


A simple diagram of a Web Client-Server architechture is represented below


![Alt Text](https://cdn-cfpof.nitrocdn.com/BlsuvUouCRMZXlRDnoReLQfXZdugMQtC/assets/images/optimized/rev-36dcb65/teachcomputerscience.com/wp-content/uploads/2020/11/Client-Server-Architecture-1.png)


Extending this concept further and adding a Database Server to the above architechture will give us the model below

<img width="864" alt="Screen Shot 2023-09-22 at 10 14 54 AM" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/554d6378-740c-4baa-b7db-e72ef09989ac">

Let's take an example to see a Client-Server communication action.


For this we will be using a commercially deployed LAMP website `www.propitixhomes.com`

on terminal, we will run the following curl command `curl -Iv www.propitixhomes.com`, please not that if curl is not present on your machine, you can install it with the following command `sudo apt install curl`

In this example, our terminal will be the `Client`, while `www.propitixhomes.com` will be the `Server`.

Below is the response from the remote server, and we can also see that the requests from the URL are being served from a computer with an ip address 75.2.115.196 on  port 80 

<img width="462" alt="curl propitihomes" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/987605e3-db58-419d-8eb0-a5b5c08a4a4a">


## Implementing a Client-Server Architechture using MySQL Database Management System.

### 1. Create and Configure two linux based server using the AWS EC2 console

Server A name - `mysql server`
Server B name - `mysql client`

<img width="1280" alt="instances" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/0b2c74ab-6857-44c3-b11d-37946a52e0db">


### 2. On the `mysql server` we will install the MySQL Server software
We will begin this by connecting terminal to the `mysql server` instance by
updating apt using the command `sudo apt update`

<img width="750" alt="apt update server" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/fef624f3-2af2-4891-b9c5-3a61bc4c09b3">


then we will install the MySQL Server sofware using the command `sudo apt install mysql-server -y`


<img width="474" alt="install MySQL Server" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/47dad58c-5a3a-44cf-b678-93c930235bf3">


afterwhich we will enable the proccess using the command `sudo systemctl enable mysql`


<img width="733" alt="Enable MySQL Server" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/275fd0d6-5bca-43ef-9af7-d67a51a717d6">


### 3. On the `mysql server` we will install the MySQL Client software
We will begin this by connecting terminal to the `mysql client` instance by
updating apt using the command `sudo apt update`

<img width="964" alt="apt update client" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/75da1a00-63f2-46cb-9414-a6a047ccef29">


then we will install the MySQL Client sofware using the command `sudo apt install mysql-client -y`


<img width="872" alt="install MySQL Client" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/a24e1c6c-a36f-42b8-a75f-3db5c9594865">


