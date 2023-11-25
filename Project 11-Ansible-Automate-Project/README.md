# Ansible-Automate Project



## Install and Configure Ansible on an EC2 Instance
For this project, this will be done on an existing `Ubuntu` instance (ubuntu 20.04 LTS)

(<img width="1252" alt="Ubuntu 20 04 LTS" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/61e2702d-b862-411c-97c5-6761d2312f83">

This is the same jenkins server in the jenkins guide above, but for this purpose we will only modify the instance name to `Jenkins-Ansible` 

<img width="920" alt="instance rename" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/e18ef244-fa10-40ea-9c1b-85b16446c4a7">

##### Creating a new repository
From our GitHub, we will create a new repository named `ansible-config-mgt`

<img width="976" alt="new repo" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/565563f3-d7c5-4522-a251-abbc360470d4">

##### Installing Ansible
As we should know, it is best practice to update our package manager before we proceed

Sincw we are working with an `Ubuntu` OS of the `Debian` distribution, we will do so with the command `sudo apt update` `sudo apt update`

<img width="721" alt="apt update" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/8f846e25-db79-418c-ab0b-322bb5fe1742">


Now we can install `Ansible` with the command `sudo apt install ansible` 

<img width="488" alt="install ansible" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/d86b5f10-1641-4b6c-b50e-b85da57d6339">



Ansible version can also be checked using the commnad `ansible --version` (this is also a way to confirm the insatallation)

<img width="821" alt="ansible --version" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/487828a9-33bd-44bf-8fc2-b63d9606e6e1">


## Configure Jenkins build job to archive your repository content every time you change it


To do this, we will:
- Create a new Freestyle project `ansible` in Jenkins and point it to your 'ansible-config-mgt' repository.
- Configure a webhook in GitHub and set the webhook to trigger ansible build.
- Configure a Post-build job to save all (`**`) files, as explained in my ansible guide documentation.

