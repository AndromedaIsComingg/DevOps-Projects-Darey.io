# Ansible-Automate Project

`Ansible` is an open source community project sponsored by Red Hat, it's the simplest way to automate IT, the suite includes software provisioning, configuration management, and application deployment functionality.

While `Jenkins` is an open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration, and continuous delivery. 


##### Reqiurements
For this project execution, the following components will be required.
1. Infrastructure - AWS
2. Jenkins-Ansible Server - Ubuntu
3. Webservers - 2 Linux RedHat Enterprise
4. Database Sever - Linux RedHat Enterprise
5. Storage Server - Linux RedHat Enterprise
6. Load Balancer Server - Ubuntu
7. Programming Language - PHP
8. Code Repository - GitHub
9. Stable network connection
10. Access to the terminal
11. VS Code + Remote Development Etension
12. A user account with sudo privileges
13. A Laptop or PC to serve as a client


##### Prerequisites
- Knowledge of how to create an EC2 Instance and how to connect to it. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/Other-Projects/blob/main/Project%204/README.md)
- Understanding of basic Unix command knowledge. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/Other-Projects/blob/main/Project%201-Linux_Pracice_Project/README.md)
- How to setup a continous Integration system with Jenkins. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/blob/main/Continuous%20Integration%20with%20Jenkins/README.md)


## Installing and Configuring Ansible on an EC2 Instance
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
- Configure a Post-build job to save all files.

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

In the "Files to archive" blank bar, fill in `**` (** saves all the file). if you want jenkins apply some particular pattern to define which files to archive, you can learn the syntax [here](https://ant.apache.org/manual/dirtasks.html#patterns)

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

<img width="1254" alt="Checkout ansible-jen" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/f5b0655d-bb91-4f5b-a3fc-e2b1dd2b8bd1">


##### Creating  Directories

- Create a directory and name it playbooks - it will be used to store all your playbook files.
- Create a directory and name it `inventory` - it will be used to keep your hosts organised.

<img width="858" alt="mkdir playbook inventory" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/48ab71a4-e146-4eaa-8be5-848528178508">

##### Creating files

- Within the playbooks folder, create your first playbook, and name it common.yml
- Within the inventory folder, create an inventory file for each environment (Development, Staging Testing and Production) dev, staging, uat, and prod respectively. These inventory files use .ini languages style to configure Ansible hosts.


<img width="859" alt="creating files" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/42b32455-1ed6-491a-bd40-f977b8e28104">


Note: Ansible uses TCP port 22 by default, which means it needs to ssh into target servers  from Jenkins-Ansible host - for this you can implement the concept of ssh-agent. Now you need to import your key into ssh-agent using: 
```
eval `ssh-agent -s`
ssh-add <path-to-private-key>
```

Please note that the above commands MUST be ran locally from any every command line interface before proceeding with logging in with the login method instructed below as an SSH-Agent, sometimes on the same CLI, one will need to run these command on every individual tab where one wants to have access as an SSH agent. 

<img width="390" alt="ssh add" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/988cce01-9b60-4ccd-8a12-6357b34f3f64">


 Now instead of logging in into the EC2 instance with the  identity file, we will be logging in using the SSH Agent with the command 
 `ssh -A ubuntu@<Public-IP>`, then persist the key on the server using `ssh-add -l`


<img width="553" alt="ssh agent" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/07aae317-e531-42ee-adc5-9dedfd856cfc">


 This means that the Ansible Server will be able to access all other instances we will be creating with the same .pem keypair (watch out for this proccess later on when we will be confirming `Ansible` installations of `wireshark` on other servers from the "Jenkins_Ansible" Server.


 Snapshot of other instances for this project using the same key pair is below
The instances include `NFS,` `db`, `webserver 1 & 2`, and `lb` 

<img width="1109" alt="snapshot instances" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/50ca0bee-f8a3-45da-b125-e2269a13c758">


##### Update your inventory/dev.yml file with this snippet of code:

```
[nfs]
<NFS-Server-Private-IP-Address> ansible_ssh_user=ec2-user

[webservers]
<Web-Server1-Private-IP-Address> ansible_ssh_user=ec2-user
<Web-Server2-Private-IP-Address> ansible_ssh_user=ec2-user

[db]
<Database-Private-IP-Address> ansible_ssh_user=ec2-user 

[lb]
<Load-Balancer-Private-IP-Address> ansible_ssh_user=ubuntu
```

<img width="704" alt="dev edit" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/6840bbb7-8ef3-4b36-b945-0de81efb8bf3">


Also notice, that your Load Balancer user is ubuntu and user for RHEL-based servers is ec2-user.


##### Create a Common Playbook
It is time to start giving Ansible the instructions on what you need to be performed on all servers listed in `inventory/dev`
In `common.yml` playbook you will write configuration for repeatable, re-usable, and multi-machine tasks that is common to systems within the infrastructure.
Update your `playbooks/common.yml` file with following code:

```
---
---
- name: update web, nfs and db servers
  hosts: webservers, nfs, db
  remote_user: ec2-user
  become: yes
  become_user: root
  tasks:
    - name: ensure wireshark is at the latest version
      yum:
        name: wireshark
        state: latest
   

# -----------------------------------------------------------

- name: update LB server
  hosts: lb
  remote_user: ubuntu
  become: yes
  become_user: root
  tasks:
    - name: Update apt repo
      apt: 
        update_cache: yes

    - name: ensure wireshark is at the latest version
      apt:
        name: wireshark
        state: latest

```

<img width="844" alt="common" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/996425f3-9b57-4e0e-8168-47117c6c7bee">



##### Update GIT with the latest code
Now all of your directories and files live on your machine and you need to push changes made locally to GitHub.
This is done by using the git add and commit commands `git add .` to add all files with changes, and `git commit -m "<commit message>"` to commit new changes

<img width="865" alt="git commit" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/f33f56fb-de53-4672-980f-492e65add1b0">


Please note that the above `add` and `commit` was carried out in the created branch `ansible-jen`

##### Push Changes and Create a Pull Request


This is done with the command `git push origin <branch-name>`. This push will automatically create a pull request in the GitHub remote remote repository

<img width="737" alt="git push" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/76c301a0-8e71-4169-8fd7-2c18440287cd">



We will receive a prompt to compare and pull, afterwhich we will click om "Create pull request", the proceed to "Merge pull request", then "Confirm merge"


<img width="952" alt="compare   pull" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/a9f7a8be-70c6-412e-8139-cf8b1de7fa5c">



<img width="902" alt="create pull" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/84326b2f-778d-4c17-94a1-1474475e8564">


<img width="942" alt="Merge pull" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/48ab1d9e-b948-4047-86f2-d6ef437c1f47">



<img width="877" alt="Merge confirm" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/5aa99487-5714-4e63-a74c-3031d679188c">



##### Checking branch `main` to confirm that files and folders have been updated
Once the push is succesfull, we expect to have the files in the Github repository updated as such

<img width="703" alt="Main updated" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/761584bb-b407-4272-859c-99883538c752">


We should also confirm that the changes in the Github repository has trigger a build in the Jenkins console

<img width="729" alt="jenkins trigger 2" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/467dcd50-f7f6-4e37-a3ef-350e0e8cacf5">


We can proceed to check the update out in the following jenkins directory on the Jenkins-Ansible Server

`/var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/`

<img width="605" alt="ls build 4" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/71e45b55-bcd6-4d1c-8a10-1389dabf4d47">


##### Updating the branch `main` locally
Since the `add` and `commit` we performed earlier was on the `ansible-jen` branch, we will switch into the main branch with the command `git checkout main` and check the status with the command `git status` and update the branch with a pull command `git pull`.

<img width="736" alt="main branch update" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/93563083-22a8-41ab-95ea-1ad746085916">


## Run first Ansible test
Now, it is time to execute ansible-playbook command and verify if your playbook actually works:

##### Setup your VSCode to connect to your instance
This where we use the `Remote Development` extension installed earlier


Connect to host, Add new ssh

<img width="833" alt="ssh config" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/a1f8a735-b9ff-4565-9f36-c6d233aa6cc2">

update the configuration as below

```
Host jenkins-ansible
  HostName <public IP>
  User ubuntu
  IdentityFile <path-to-keypair>
  ForwardAgent yes
  ControlPath /tmp/ansible-ssh-%h-%p-%r
  ControlMaster auto
  ControlPersist 10m
```


<img width="635" alt="host config" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/b18b64bc-0e37-4adb-a20c-1c1b931cf846">

Now we have a remote login from VS code of our `Jenkins-Ansible` instance, from where we will access the ubuntu user files from the home directory `/home/ubuntu/`


<img width="831" alt="home dir" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/09da2da8-56ec-4ec2-8657-74dd5f86ac24">


##### Now run your playbook using the command:
`ansible-playbook -i /var/lib/jenkins/jobs/ansible/builds/<build-number>/archive/inventory/dev.yml /var/lib/jenkins/jobs/ansible/builds/<build-number>/archive/playbooks/common.yml`


Please note that all SSH Agent commands has to be ran on the "Remote Development" extension new window (locally) as a new agent 


<img width="956" alt="wireshark install" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/61830854-676e-4241-8e8c-7c0a876b3583">


##### Confirming Installations
We can now login into the servers to check if "wireshark" have been installed on the servers using the command `which wireshark` or `wireshark --version`


let's check on `webserver-1` (a RedHat instance)

<img width="759" alt="wireshark on web1 redhat" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/ab27290f-fc96-48d8-8e21-a94bf8d77732">


and on our load balancer, `lb` (an ubuntu instance)

<img width="682" alt="wireshark lb ubuntu" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/690119e7-2b91-46b9-8cf9-38aaed9a72cb">


##### This shows a successful `Ansible` Automation configuration alongside `Jenkins` facilitating continuous integration, and continuous delivery.




The overall Automation setup looks like the diagram below

<img width="908" alt="Ansible updatd schematic" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/94bcfcbd-f911-4037-b9eb-ff1c5b683dfe">



---------------------------------![Alt Text](https://cssbud.com/wp-content/uploads/2021/05/thanks-for-your-time.gif)---------------------------------------------




