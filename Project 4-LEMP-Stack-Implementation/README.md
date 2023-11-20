# LEMP-Stack-Implementation

##### LEMP is a web stack which comprises of 
- LINUX Operating Ststem
- NGINX Web Server
- MySQL for Database Management
- PHP to Empower Server-side Functionality

It is similar to LAMP Stack with the major difference beineg that the web server in LAMP Stack, APACHE, is being replaced by NGINX.
We will start this implementation by launching a Linux Ubuntu operating system from our AWS EC2 compute service.

## AWS Account & EC2 Instance
###### Creating an AWS Account and spinning an EC2 instance.
From the AWS web platform `AWS.Amazom.com` we will sign up and create an account, after which we will check for EC2 in the compute services.

For this purpose an instance was created which was named `For Instance`
<img width="1280" alt="AWS Acct" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/14e2925b-50d3-4442-8bae-1dbc8768da8a">


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

## Connecting to the EC2 Instance
###### Connect to the EC2 instance by running the command `ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>`
This connects terminal to the EC2 instance using SSH, which is a Secure Shell network communication protocol that enables two computers to communicate.

<img width="598" alt="starting ubuntu" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/26d1bd55-66c9-4463-b6f2-404f2108b137">

## Installing Nginx Web Server
The Nginx web server will serve to display the web pages to visitors,
in order to install this we will be using the apt package manager along side the sudo command so as to grant admin privilages.
The package was installed using the following command `sudo apt install nginx`
Please note that the `-y` flag is to handle future prompts of yes/no

<img width="1280" alt="Nginx install" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/c04e87bf-e160-4555-875d-bb1815d75d4b">

## Verifying Nginx
The instalation of Nginx can be confirmed using the following command to be assured that it is running properly.
`sudo systemctl status nginx`

<img width="883" alt="Nginx status" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/ef0066b7-1e4e-4fa3-9d59-691664bc026b">

## Editing Inbound Rule
###### Now we will edit inbound rule such that connection through port 80 is allowed and from any ip address.<img width="1271" alt="editing inbound rule" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/b90f17dd-51aa-422a-a2e3-f19a52b4b278">


## Accessing Server
##### Since our server is up and running we will try to access it from our local machine and also from a web browser
Accessing via the local machine, we are going to access via the IP and also via DNS name both of which will be carried out with the "curl command"
Using the commands 
```html
curl http://127.0.0.1:80

curl http://localhost:80
```
<img width="747" alt="curl ip   DNS" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/4251e216-7135-4ed2-b2fc-3f8e65ced545">

##### Checking if the Nginx server can respond to internet requests via a web browser.
This will be done using the public IP.
We can use the following command to fetch the public IP from the local machine, instead of going on AWS EC2 instance using the command
'curl -s http://169.254.169.254/latest/meta-data/public-ipv4'

<img width="633" alt="public IP check" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/29264ebb-f743-4ac5-871d-f1c869395f58">

Now that we have the public IP, we can now use it with the following command to check if Nginx responds to internet requests.
Using a web browser, we will enter the public IP into the address bar with or without specifying port 80
this is because all web browsers use port 80 by default.

<img width="1023" alt="welcome Nginx" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/8473287b-8739-4ab1-8112-e966fcd6cf0f">


## Installing MySQL
###### Used apt to install this software using the command `sudo apt install mysql-server`
###### The sudo command gives admin previlages and when prompted, installation was confirmed by typing y and then pressing enter.
<img width="1222" alt="sudo MySQL install" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/82feb343-7c33-4cce-851c-0a29fd3d31df">


###### After installation, logged into the Mysql Console with the command `sudo mysql`
<img width="561" alt="MySQL Start up" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/605ca9d8-7387-493e-ab01-18536f1da7bd">


##### Password was set for root user using the command `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`
<img width="661" alt="user password" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/a8c63d47-187a-4499-8b24-adc24fe7a93e">


##### When done, tested to login into the MySQL console by using the command `sudo mysql -p`
##### The -p flag prompts for password after the root user password has been changed.
##### The "mysql> exit" command was used to exit the MySQL console.

<img width="580" alt="login test   exit" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/ed835c52-1429-4213-b3a9-4c8eac184d0c">

## Installing PHP
Now that we have Nginx to serve web services and MySQL to handle database,

we can now procede to install PHP to process code and generate dynamic content for the web server.

To use an Nginx server, we will need to install some external programs for it to communicate with PHP.

They are `php-fpm` (PHP fastCGI process manager) and `php-mysql`, a PHP module that helps PHP to communicate with MySQL-based database.

These two packages can be installed using the command `sudo apt install php-fpm php-mysql`

<img width="920" alt="two external progs" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/9251a042-9870-467c-924d-385420b4ce24">

## Configuring Nginx to Use PHP Processor
Similar to the use of virtual hosts in Apache, Nginx web server have server blocks can also be configured to accomodate configuration details

and host more than one domain on a single server.

To acheive this we will have to create a new working directory leaving var/www/html in its place as the default directory

which will be served if client's directory does match any other site.

we will name this directory "projectLEMP" which will be created with the following command `sudo mkdir /var/www/projectLEMP`

<img width="432" alt="mkdir projLEMP" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/794e7552-bc31-4f65-bf63-6a6e0df5e9ae">

Then we assign ownership which will reference to the current system user with the command `sudo chown -R $USER:$USER /var/www/projectLEMP`

<img width="524" alt="chown projLEMP" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/85868654-766a-4815-a4da-5aac9123cfd1">

Now using any command line editor, we will open a new configuration file in Nginx's site-available directory using the command

`sudo nano /etc/nginx/sites-available/projectLEMP`, inside which we will paste the following lines of code,

and exit with ctrl+x since we are using the nano editor.

```html
#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}'
```

<img width="430" alt="nano edit" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/87bfc38a-ceed-461e-a58a-44586405a7e3">

##### Activating Configuration
This is done by linking the configuration file from the Nginx's sites-enabled directoy

using the code `sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/'

This prepers Nginx to use the configuration file when next it is loading.

Also, we will be testing this configuration using `sudo nginx -t`

<img width="740" alt="enable test Nginx" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/3d7e7295-3d73-4858-895e-354b21f2752a">


##### Unlinking port 80 & Reloading Nginx

For this too run, Nginx host that was previosuly configured to run on port 80 needs to be diabled and the Nginx reloaded

we will carry out those operations using the following commands.

`sudo unlink /etc/nginx/sites-enabled/default` and `sudo systemctl reload nginx`

<img width="555" alt="unlink" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/b82f882e-7edb-455d-841e-84ce41ff4921">


<img width="405" alt="realod" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/96c14619-70ac-49c5-bbb7-bff76347f0d9">


##### Testing Server Block
Now we will create an index.html file in the newly created empty directory to test if our new server block is working as expected

we will do that using the commad `sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`

<img width="1280" alt="echo" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/65532bae-eae9-4c75-87e5-e604b0c260cf">

Now from our web browser we can confirm this by entering the public IP and see if the echo message gets displayed.

<img width="791" alt="web test active" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/2f5fddb7-91bb-4cfc-b362-bf856ea7eee2">

## Testing PHP with Nginx
Now that out LEMP is fully operational, we will test to validate that Nginx can correctly hand .php files off to our PHP processor.

We will be doing this by creating a PHP file named "info.php" in our document root using the nano text editor using the following command
`nano /var/www/projectLEMP/info.php` after which we will be pasting the following valid lines of code.
```html
<?php
phpinfo();
```

<img width="260" alt="nano php" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/b9002430-220a-4d0c-aadf-f30b3bcee49c">

Now we can access the PHP page using a web browser by inputing the public IP address followed by `/info.php`

<img width="1089" alt="php page" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/7aeca848-e48c-4cb3-9b2a-a2285fed3b2d">

It is of best practice to remove the newly created PHP file as it contains sensitive information about the PHP environment.

We will be doing that using the `mv` command  `sudo rm /var/www/your_domain/info.php`

Although this file can always be regenerated when needed.

<img width="468" alt="removing php file" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/61d8d128-775c-4042-9e60-78e399ea8951">

## Retrieving Data From MySQL Database With PHP
To execute this, first we will have to connect to the MySQL console using the root privilage using the command `sudo mysql`

Then we will create a database called example_database and a user called example_user with a password `passWord1` using the commands

```html
mysql> CREATE DATABASE `example_database`;
```
 and
 
 ```html
mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
```

<img width="670" alt="create database user   PW" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/84a72869-8198-4ea4-b518-ec3c4bd729de">


Now we will need to give our user permission over the "exampl_database" database that was created.

This is done so that the user will have full privilages over the database and is done with the command mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';  after which we will type "exit" and enter to leave the MySQL console.

<img width="447" alt="grant accss user" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/ace14cd6-bf68-4bad-8d92-1e8e1e28ab3b">


Now we will test if the user has proper permission to the database by logging into mySQL again and using the custom user credentials

We will do so using the command `mysql -u example_user -p` the -p flag in this command is to prompt for password, which will be thesame

password used when creating the user account.

<img width="558" alt="MySQL login costum" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/6df87e04-64da-4929-9fcd-edf8c7495c7e">


To confirm that we have access to database, we will use the following command
```html
`mysql> SHOW DATABASES;`
```

<img width="173" alt="show database" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/9b74ecff-1bf2-46c8-a0af-8c60fee2c779">

From the MySQL console we are now going to create a table named to-do list by running the following statement.

`CREATE TABLE example_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));`

 Then we will insert a few rows of content into the created table using the statement 
 
 `INSERT INTO example_database.todo_list (content) VALUES ("My first important item");`

  `INSERT INTO example_database.todo_list (content) VALUES ("My second important item");`

 `INSERT INTO example_database.todo_list (content) VALUES ("My third important item");`

 <img width="655" alt="todo add" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/2c0b269f-7c16-440d-b750-177faf5da413">


 Now we will have to confirm if the data was successfully added to the table using the command
 
 `SELECT * FROM example_database.todo_list;`

 <img width="357" alt="table display" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/b9425514-6edf-4da4-ba3c-330890576c48">

Now we can exit MySQL like we did before by typing "exit" + enter

Now in the costum we root directory, we are going to create a PHP script which we will name `todo-list.php`

that will connect to MySQL and query for the created content.

For this, we will be using the VI editor with the following command

`vi /var/www/projectLEMP/todo_list.php` and pasting the following lines of code 

```html
<?php
$user = "example_user";
$password = "PassWord.1";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}
```

and we will exit the VI editor with the command `:wq!`


<img width="537" alt="vi todo-list" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/e7f405b3-76a0-4c10-b885-4beea65d429f">

 Now we can check from our web browser using the same method of using the public IP or DNS + /todo_list.php in the format
 
 `http://<Public_domain_or_IP>/todo_list.php`

 <img width="430" alt="todo_list web display" src="https://github.com/AndromedaIsComingg/LEMP-Stack-Implementation/assets/140917780/587e5903-4dbb-44f7-a245-370116439843">

 Hurray!!! This result indicates the our PHP environment is ready to connect and interact with MySQL server and our LEMP Stack has been successfully configured.
 
---------------------------------![Alt Text](https://cssbud.com/wp-content/uploads/2021/05/thanks-for-your-time.gif)---------------------------------------------

