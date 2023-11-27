# Ansible-Automate Project



## Install and Configure Ansible on an EC2 Instance
For this project, this will be done on an existing `Ubuntu` instance (ubuntu 20.04 LTS)

<img width="1252" alt="Ubuntu 20 04 LTS" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/61e2702d-b862-411c-97c5-6761d2312f83">

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


## Configuring Jenkins to retrieve source codes from Github using Webhooks


In this part, we will configure a simple Jenkins job/project. This job will be triggered by GitHub Webhook and will execute a build task to retrieve codes from Github and store it locally on Jenkins Server.

##### Enabling Webhook

This is done in the GitHub Repository Settings


Fill the `Paylaod URL` with `<jenkins-URL+port>/github-webhook/`, select "Content type" `application/jason'

<img width="1192" alt="git webhook" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/4f8f710a-93b5-4560-8120-05d9d9d38066">


## Configure Jenkins build job to archive your repository content every time you change it


To do this, we will:
- Create a new Freestyle project `ansible` in Jenkins and point it to your 'ansible-config-mgt' repository.
- Configure a webhook in GitHub and set the webhook to trigger ansible build.
- Configure a Post-build job to save all (`**`) files, as explained in my ansible guide documentation.

<img width="1163" alt="Freestyle" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/96b14410-469f-4472-b1b0-72bc5c87cbed">


Give the Job a name and under source code management, select Git and paste the repository URL

<img width="1266" alt="Repo URL" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/f1d8202a-51ec-4dda-87c7-fa2eb083207d">


Add Credentials, Jenkins (user/password) so Jenkins could access files in the repository.

<img width="911" alt="jen cred" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/05fb7794-6a89-4607-b17a-24627613d07a">


##### Build Test

Saving the above configuration takes us back to the dashboard where we will use the Build Now option to test the congiguration

If you see a green tick sign before #1 at the lower left side of the console, it means everything was configured correctly and the build was successfull.

<img width="842" alt="build 1 or 2" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3ec490d9-2cf7-4cdf-9b31-60964981d649">


Please not that if you have a failed biuld you may need to go back to `configuration` and change "Branch Specifier" from `master` to `main` or any corresponding name of branch.

<img width="1218" alt="Branch Specifier" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/c22edfdc-640c-43f2-a1f6-2b313f8b5328">


Also, if you have an error which looks like `HTTP ERROR 403 No valid crumb was included in the request`

Then go back to Dasboard, Manage Jenkins, Configure Global Security, scroll down and check "enable proxy compactibility"


##### Configuring Github to trigger Build Jobs Automatically

We will do this by selecting the job (ansible) then "configure", go to the "Build Triggers" tab, this is where we will check the option "GitHub hook trigger for GITsm polling"

<img width="876" alt="hook trigger" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/f5267aff-e416-440e-bfc3-f3990ec28875">


Configure "Post-build Actions" to archive all the files - files resulted from a build are called "artifacts".

Move to the "Build Environment" tab, click the "Add post-build action" dropdown and select "Archive the artifacts"

In the "Files to archive" blank bar, fill in `**`

<img width="878" alt="Archive artifacts" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/834b7342-68b1-4f65-9b12-e89187a69294">


##### Checking if auto biuld configuration is effective

This is done by editing any content in the GitHub repository, for this we will choose the README markdown file, where we will add a few text and check to see if it triggers an auto build in Jenkins

<img width="1280" alt="ReadME edit 4 trigger" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/97596058-941d-45fe-89a0-5ba4ca7ebf77">


<img width="693" alt="auto trigger success" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/c66b242a-f422-47b8-b561-0bf9475ea6dd">


The above image shows that we have an auto-trigger success.


##### Checking if Jenkins saves the files (build artifacts) in following folder

This is confirmed by checking the following path `sudo ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/`

<img width="698" alt="terminal change confirmatn" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/f243f2e9-eeb6-459b-8df7-b69e73e41ff5">


Since setup is okay, this is the blueprint of our setup

<img width="973" alt="Schematic" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/e6354214-d4bf-41ff-b945-72acef6d5b23">


Please note that every time you stop/start your Jenkins-Ansible server - you have to reconfigure GitHub webhook to a new IP address, in order to avoid it, it makes sense to allocate an Elastic IP to your Jenkins-Ansible server. Also note that Elastic IP is free only when it is being allocated to an EC2 Instance, so do not forget to release Elastic IP once you terminate your EC2 Instance.


## Preparing your development environment (IDE)

For this project, we will be using Visual Code Studio, you can get it [here](https://code.visualstudio.com/download)


After you have successfully installed VSC, configure it to connect to your newly created GitHub repository. For guide on how to do this, please check my earlier documentation [here](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/tree/main/Project%202-Git-Project)


##### Installing "Remote Development" Extension
This is an extension pack that lets you open any folder in a container, on a remote machine, or in WSL and take advantage of VS Code's full feature set.


<img width="1133" alt="Remote development" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/7fb45e2c-fe9e-4c17-8655-f9fc23124464">


<img width="1279" alt="VSCode opened" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/e627e814-d665-4e1e-b620-81388c336cf9">

##### Creating a new branch and checking out into it
For this, we will be creating a new branch called "ansible-jen", using the command `git checkout -b ansible-jen`


