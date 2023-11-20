# Lamp-Stack-Implementation
Project 3


## AWS Account & EC2 Instance
###### Created an AWS Account and spinned an EC2 instance named `For Instance`
<img width="1280" alt="AWS Acct" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/14e2925b-50d3-4442-8bae-1dbc8768da8a">


## Private Key
###### Created and downloaded a private key named `1stkey`
###### The .pem file was saved in the "Downloads" folder as shown below

<img width="320" alt="pem file in dwnlds" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/d73e3fac-39ac-42ef-a5d3-844018d53cbe">


###### From Terminal, working directory was changed to the "Downloads" folder
<img width="272" alt="cd Downloads" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/f0d64650-0ac8-40d6-b2ae-5177940e2a91">

###### From Terminal, permission was changed for the private key.
<img width="412" alt="changing permission for private key" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/6890a6f6-da94-49d0-a2e5-cc5894f8888d">

## Connecting to the EC2 Instance
###### Connected to the EC2 instance by running the command `ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>`
<img width="598" alt="starting ubuntu" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/26d1bd55-66c9-4463-b6f2-404f2108b137">


## Installing Apache & Firewall
###### Updated a list of packages in package manager
###### Updated these packages with the command `sudo apt update` with the `sudo` giving admin privelages.
###### After which the Apache package was installed using the `sudo apt install apache2` command
<img width="735" alt="sudo apt and apache2 instl" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/f4be9849-17c6-444a-ba45-67d2d818a64e">


## Verifying Apache
###### Verified that Apache was running as a service in the os with the command `sudo systemctl status apache2`
<img width="653" alt="apache2 verifucation" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/9d7c1cd6-cd36-4dbe-b7ac-fb0a8565d137">


## Editing Inbound Rule
###### Edited inbound rule such that connection through port 80 is allowed and from any ip address.<img width="1271" alt="editing inbound rule" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/b90f17dd-51aa-422a-a2e3-f19a52b4b278">


## Accessing Server
###### Accessed server locally on Ubuntu shell using the `curl` command as shown below
<img width="917" alt="curl local host check" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/127203f3-61eb-4eb9-bd9b-15acc62df7e5">

###### Tested the Apache HTTP Server with a web browser. This done by using the public ip in the address bar.
<img width="949" alt="apache test web" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/93072342-9964-44ef-9034-5f8a25c2bc64">


## Installing MySQL
###### Used apt to install this software using the command `sudo apt install mysql-server`
###### The sudo command gives admin previlages and when prompted, installation was confirmed by typing y and then pressing enter.
<img width="1222" alt="sudo MySQL install" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/82feb343-7c33-4cce-851c-0a29fd3d31df">


###### After installation, logged into the Mysql Console with the command `sudo mysql`
<img width="561" alt="MySQL Start up" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/605ca9d8-7387-493e-ab01-18536f1da7bd">


##### Password was set for root user using the command `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`
<img width="661" alt="user password" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/a8c63d47-187a-4499-8b24-adc24fe7a93e">


##### When done, tested to login into the MySQL console by using the command `sudo mysql -p`
##### The -p flag prompts for password after the root user password has been chnaged.
##### The "mysql> exit" command was used to exit the MySQL console.

<img width="580" alt="login test   exit" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/ed835c52-1429-4213-b3a9-4c8eac184d0c">


## Istalling PHP
##### In order to proccess codes to display dynamic content to the end users, PHP is the package to install.
##### In addition to PHP, we install other features like, php-mysql and libapache2-mod-php
##### These 3 packages were insatalled at once with the command `sudo apt install php libapache2-mod-php php-mysql`
<img width="1082" alt="PHP   co install" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/ccc93fde-09c5-4c14-9e81-59d20cbb1670">

##### Afterwhich the version of PHP was confirmed using the command `php -v` and the verision is 8.1.2
<img width="563" alt="PHP version" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/06ad99df-10a1-4037-8dfa-af2760f14958">


##### Changing the order of files in the default directory index such that index.php file will take precedent over index.html
##### This was done using the command `sudo vim /etc/apache2/mods-enabled/dir.conf`
<img width="715" alt="Vim command" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/54b1ced0-0364-499c-a80a-0967edce9611">


##### This order was edited using the insert mode in the vim editor.
##### pressing "i" on the keyboard takes us to the insert mode & "esc" to exit it
##### Changes were written and vim was exited with the command `:wq!`
<img width="708" alt="Vim" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/ec0e8c3e-ae9e-4bde-8897-e999fe2f2fe8">


##### After saving and closing the file, Apache was restarted for changes to take effect
##### Restart was done with the command `sudo systemctl reload apache2`
<img width="420" alt="apache reload" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/4a21badb-0947-4040-bf14-b8a12541555b">

##### Next, we will creating a PHP script to test that PHP is installed correctly and configured on the server. 
##### The file name is "index.php" and the directory for this file was also created with the `mkdir` command.
<img width="577" alt="creating index php   dir" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/a09fec5c-2e45-4b07-b6aa-01a04e8b2df3">

##### Inside the vim editor, the following valid PHP code was added to the newly openned blank "index.php" file
##### Changes were written and vim was exited with the command ":wq!"
<img width="238" alt="adding php code" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/71a580de-64a4-454d-8644-cc0a15ceee2e">

##### Removing the Created PHP file
##### After confirming all relevant information via the PHP file, the newly created PHP file was further removed
##### as it contains sensitive information about the PHP environment and the Ubuntu Server.
##### That was done with the command `sudo rm /var/www/projectlamp/index.php`
<img width="479" alt="removing  php file" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/c3927e8e-8a76-4c0e-89d8-b20691212f8d">


## Creating a virtual host for the website using Apache
##### We will be doing this using the earlier created directory
##### Then we will assign ownership of the environment with the USER environment variable using the command `sudo chown -R $USER:$USER /var/www/projectlamp`
<img width="549" alt="chown" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/4601ab86-4822-4a95-a743-3f3963d400fe">


## Creating a configuration file
##### Created and edited a new configuration with the vi editor in Apache's site-available directory using the code `sudo vi /etc/apache2/sites-available/projectlamp.conf:`

<img width="581" alt="vi for  conf code" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/4ed2a4bc-d4d0-4995-b52f-1cf3f1bedfb0">

##### Changes were written and vim was exited with the command ":wq!"


<img width="414" alt="vi  conf vi" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/7a0cf692-ab19-468a-8cfd-f1b98c770f44">



##### The `ls` command was used list and confirm that the new files are available in the site-available directory
<img width="485" alt="ls" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/538e1f4e-e44d-42b7-8218-6c61ee60a54b">

##### The a2ensite command was then used to enable the virtual host using the command `sudo a2ensite projectlamp`
<img width="422" alt="enable virtual host   reload" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/b6ea6c37-b9ea-4372-abe8-e4456592162d">


##### The default website that comes with Apache was disabled using the code `sudo a2dissite 000-default`
<img width="392" alt="disable defaul web" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/0244b473-6926-4b1e-b7ae-837166046fac">

##### The configuration file was confirmed to not contain any syntax error using the following command `sudo apache2ctl configtest`
<img width="395" alt="syntax errror" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/15a5bc22-6c98-49b4-a37e-7721aac31f3b">


##### Apache was relaoded so that changes can take effect, this was don using the command `sudo systemctl reload apache2`
<img width="420" alt="apache reload" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/5e170e51-61d2-4e97-b3e3-3c0a7b4120e5">

##### To confirm that the virtual host is working as expected, an index.html file was created in the same directory
##### Using the echo command to display the text "Hello LAMP from hostname" using the following command
##### `sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`
<img width="1239" alt="sudo echo php" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/809504df-ad31-472e-9b11-7db7d3569c5b">

##### This was finally confirmed on the web browser using the format `http://<Public-IP-Address>:80` (testing usinsg the public ip address)
<img width="1275" alt="web test ip" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/0179a91c-dd53-46ad-b542-c5375297baa3">


##### Also with the format `http://<Public-DNS-Name>:80` (testing using the public DNS)
<img width="1280" alt="web test dns" src="https://github.com/AndromedaIsComingg/Lamp-Stack-Implementation/assets/140917780/fa12acc7-14e6-4333-9966-6a156cea7988">


---------------------------------![Alt Text](https://cssbud.com/wp-content/uploads/2021/05/thanks-for-your-time.gif)---------------------------------------------
