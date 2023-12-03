# Ansible Refactoring & Static Assignments (Imports and Roles)

`Ansible` is an open source community project sponsored by Red Hat, it's the simplest way to automate IT, the suite includes software provisioning, configuration management, and application deployment functionality.

While `Jenkins` is an open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration, and continuous delivery. 


##### Reqiurements
For this project execution, the following components will be required.
1. Infrastructure - AWS
2. Jenkins-Ansible Server - Ubuntu
3. Webservers - 2 Linux RedHat Enterprise
4. Webservers (UAT) - 2 Linux RedHat Enterprise
5. Database Sever - Linux RedHat Enterprise
6. Storage Server - Linux RedHat Enterprise
7. Load Balancer Server - Ubuntu
8. Declarative Language - YAML
9. Code Repository - GitHub
10. Stable network connection
11. Access to the terminal
12. VS Code + Remote Development Etension
13. A user account with sudo privileges
14. A Laptop or PC to serve as a client


##### Prerequisites
- Knowledge of how to create an EC2 Instance and how to connect to it. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/Other-Projects/blob/main/Project%204/README.md)
- Understanding of basic Unix command knowledge. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/Other-Projects/blob/main/Project%201-Linux_Pracice_Project/README.md)
- How to setup a continous Integration system with Jenkins. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/blob/main/Continuous%20Integration%20with%20Jenkins/README.md)
- How to setup an Ansible Automate Project. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/edit/main/Project%2011-Ansible-Automate-Project/README.md)



## Jenkins job enhancement

Before we begin, let us make some changes to our earlier Jenkins job - now every new change in the codes creates a separate directory which is not very convenient when we want to run some commands from one place. Besides, it consumes space on Jenkins server with each subsequent change. Let us enhance it by introducing a new Jenkins project/job - we will require `Copy Artifact` plugin.


##### Creating a new directory in the `Jenkins-Ansible` server
This directory will be named `ansible-config-artifact, this will be created in the home directory `/home/ubuntu/ansible-config-artifact` using the command `sudo mkdir /home/ubuntu/ansible-config-artifact`. In this directory, we will be storing all artifacts after each build.


##### Granting permissions to the directory
we will be using the command `chmod -R 0777 /home/ubuntu/ansible-config-artifact` to grant permission to the the created directory so that Jenkins can save file there.

<img width="981" alt="Create dir and 0777" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3dee6cb1-2583-49f9-abab-615b354ee24b">


##### Installing the Copy Artifact Plugin
This in done in the Jenkins web console Dashboard to : 


Manage Jenkins -> Plugins -> on Available plugins tab search for Copy Artifact, check the box and install this plugin without restarting Jenkins

<img width="1179" alt="Artifact plugin" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/02c4facc-1abd-441e-8591-9a947359e169">


##### Creating a New Freestyle Project
From the Jenkins web console, create a new Freestyle project and name it save_artifacts.

<img width="718" alt="save_artifacts" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/26add04e-63a7-4d8c-bedf-fd5cd07cffb6">


##### Configuring the `save_artifacts` job

- From `General` check the "Discard old builds" option and set `Max # of builds to keep` to 2 (You can configure number of builds to keep in order to save space on the server, for example, you might want to keep only last 2 or 5 build results.)


  <img width="886" alt="discard old build" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/6cc56b09-824f-4ae6-92bc-5caf2b25d3f2">


- From `Build Triggers`, check `Build after other projects are built` and set `Projects to watch` to `ansible` (This will make this project to be triggered by completion of the existing `ansible` project)


<img width="770" alt="build triggers" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/5617a928-f616-47a7-8ce0-c0fad2435883">

- Setting Files to Copy and  Configuring Path
  The main idea of `save_artifacts` project is to save artifacts into `/home/ubuntu/ansible-config-artifact` directory. To achieve this, we will create a Build step and choose "Copy artifacts from other project", specify "ansible" as a source project and `/home/ubuntu/ansible-config-artifact` as a target directory. In the "Artifacrs to copy" blank bar we will enter `**` (** copies all the file). if you want jenkins apply some particular pattern to define which files to copy, you can learn the syntax [here](https://ant.apache.org/manual/dirtasks.html#patterns)


<img width="984" alt="artifacts to copy" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/bafe0306-31cb-44a0-931b-24eb2d642b9e">


##### Testing the Job
Test your set up by making some change in README.MD file inside your ansible-config-mgt repository (right inside main branch).


<img width="1055" alt="README edit" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/b147358e-8b46-449c-a096-b755ac0bec74">


If both Jenkins jobs have completed one after another - you shall see your files inside /home/ubuntu/ansible-config-artifact directory and it will be updated with every commit to your main branch.


Checking Build in the `ansible` job


<img width="740" alt="build 2" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/f9245eb0-5c7f-4a0f-83de-3a93af12a917">


Checking Build in the `save_artifacts` job


<img width="541" alt="build 2 copied" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/ed29453a-7769-4130-b4fd-9956a808100f">

##### CHecking to confirm the copied files

These files will be founds the the directory `/home/ubuntu/ansible-config-artifact`. We will check with the command `sudo ls /home/ubuntu/ansible-config-artifact`


<img width="567" alt="checking files" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/fd09fb7d-93cc-452d-bb63-e4f5a079384d">


Now our Jenkins pipeline is more neat and clean!!!


## Refactor Ansible code by importing other playbooks

Let see code re-use in action by importing other playbooks.


Before starting to refactor the codes, ensure that you have pulled down the latest code from main branch, and create a new branch, name it `refactor`.


This will be done with the command `git checkout -b refactor`


<img width="799" alt="refactor" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/b1c82241-bf2f-43c5-82e2-40f522e82f8c">


##### Creating Files and Folders

Within playbooks folder, create a new file and name it `site.yml` - This file will now be considered as an entry point into the entire infrastructure configuration. Other playbooks will be included here as a reference. In other words, site.yml will become a parent to all other playbooks that will be developed. Including `common.yml` that you created previously.


This is done with the command `touch playbooks/site.yml`



Create a new folder in root of the repository and name it `static-assignments`. This folder is where all other children playbooks will be stored. This is merely for easy organization of your work. It is not an Ansible specific concept, therefore you can choose how you want to organize your work. This will be done with the command `mkdir static-assignments`


After this folder is created, we will move our existing `common.yml` file into the newly created `static-assignments` folder. This will be done with the command `mv playbooks/common.yml static-assignments`


<img width="825" alt="create file and foldrs" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/ddeadd95-6beb-4bac-a34f-1b98b689829b">


Inside the `site.yml` file, import `common.yml` playbook


Use the code below inside the `site.yml` file

```
---
- hosts: all
- import_playbook: ../static-assignments/common.yml
```

The code above uses built in `import_playbook` Ansible module.

<img width="833" alt="site yml code" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/6f591b29-50a2-4993-bc76-de27aa877d2f">


Our overall folder structure in the root of the repository should look like this


├── static-assignments
│   └── common.yml
├── inventory
    └── dev
    └── stage
    └── uat
    └── prod
└── playbooks
    └── site.yml

##### Run ansible-playbook command against the dev environment

Since we need to apply some tasks to your dev servers and wireshark is already installed, we can go ahead and create another playbook under static-assignments and name it `common-del.yml`. In this playbook, we will configure deletion of wireshark utility with the following code, and the file will be created with the command `touch static-assignments/common-del.yml`


```
---
- name: remove wireshark (yum)
  hosts: webservers, nfs, db
  become: yes
  tasks:
    - name: remove wireshark
      yum:
        name: wireshark
        state: removed

- name: update LB server (apt)
  hosts: lb
  remote_user: ubuntu
  become: yes
  become_user: root
  tasks:
    - name: delete wireshark
      apt:
        name: wireshark-qt
        state: absent
        autoremove: yes
        purge: yes
        autoclean: yes
```


<img width="871" alt="common-del" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/de125321-e866-411c-86a0-daaac933158e">



##### update `site.yml`
The file will be updated with the code below since we have a new playbook to run
`- import_playbook: ../static-assignments/common-del.yml` instead of `common.yml` and run it against dev servers:


##### Update GIT with the latest code

Now all of your directories and files live on your machine and you need to push changes made locally to GitHub. This is done by using the git add and commit commands git add . to add all files with changes, and git commit -m "<commit message>" to commit new changes


For more detailed guide on how this works. please visit my ealier documentation [here](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/blob/main/Project%2011-Ansible-Automate-Project/README.md)


<img width="881" alt="git add commit" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/86415cd1-284e-499b-b810-b49251215525">


Please note that the above add and commit was carried out in the created branch `refactor`

##### Push Changes and Create a Pull Request

This is done with the command git push origin <branch-name>. This push will automatically create a pull request in the GitHub remote remote repository


<img width="904" alt="git push refactor" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/b507d554-688c-447e-a888-a74ba5f5cd95">


We will receive a prompt to compare and pull, afterwhich we will click on "Create pull request", the proceed to "Merge pull request", then "Confirm merge"


<img width="1275" alt="pull req compare" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/866f4714-c6b5-4580-9fd8-556964fe5478">




##### Checking branch main to confirm that files and folders have been updated

Once the push is succesfull, we expect to have the files in the Github repository updated as such


We should also confirm that the changes in the Github repository has trigger a build in the Jenkins console


<img width="752" alt="build merge" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/7edf531a-7d61-4dde-951f-5cad0b859a1e">


A copy also has been made in the `save_artifacts` job as the build was also triggered


<img width="736" alt="save art build merg" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/107dae29-a2eb-4d34-a609-34eb8e276d0b">


We can proceed to check the update out in the following jenkins directory on the Jenkins-Ansible Server

`/var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/` and `/home/ubuntu/ansible-config-artifact`


<img width="503" alt="files check" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/5f1ab14d-d5d5-4bc1-8cda-3bf89de6ca45">




Now we are are good to run our playbook!!!


We will be runnning it from our preferred IDE, `VS Code`, using the `Remote Development` extension.

For guide on how to use and get these, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/blob/main/Project%2011-Ansible-Automate-Project/README.md)



To run our newly created `common-del.yml` file against the dev servers in the `dev.yml` file, we will first change directory into the path below with the command


`cd /home/ubuntu/ansible-config-artifact`


and initialize the two files (remember that `common-del.yml` is the file carrying the code for the deletions, but we only instructed `site.yml` file to import `common-del.yml` files and hence, the instructions in it)


ansible-playbook -i inventory/dev.yml playbooks/site.yml


<img width="863" alt="play book rem wireshark" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/e12caae4-e4c9-4657-96be-89d3af21ba16">


We can now run the command `which wireshark` or `wireshark --version` on the dev servers to confirm that wireshark has been removed (remember that we can access any of the dev servers from our `Jenkins-Ansible` instance with the SSH agent privileges using 


`ssh ubuntu@<public-IP>` (for ubuntu instance) and `ssh ec2-user@<Public-IP>` (for RedHat instance)


<img width="562" alt="wireshark not found" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3d800e0f-d739-42bc-ba58-41a4d35288e0">


## Configure UAT Webservers with a role 'Webserver'

We have our nice and clean dev environment, so let us put it aside and configure 2 new Web Servers as uat. We could write tasks to configure Web Servers in the same playbook, but it would be too messy, instead, we will use a dedicated role to make our configuration reusable.

- Launch 2 fresh EC2 instances using RHEL 8 image, we will use them as our uat servers, so give them names accordingly - `Web1-UAT` and `Web2-UAT`.


<img width="758" alt="web-UAT instances" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/2eb1f042-5fea-4ca0-b8b2-b659292acf33">


- To create a role, you must create a directory called roles/. We will create it locally in our existing `ansible-config-mgt/` directory.

- Create the following folder/files structure


└── webserver
    ├── README.md
    ├── defaults
    │   └── main.yml
    ├── handlers
    │   └── main.yml
    ├── meta
    │   └── main.yml
    ├── tasks
    │   └── main.yml
    └── templates


<img width="978" alt="folder structure" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/f87f15aa-4a93-495a-868c-3fe3b3a762b1">


##### Updating Inventory

Update the inventory ansible-config-mgt/inventory/uat.yml file with IP addresses of your 2 UAT Web servers


```
[uat-webservers]
<Web1-UAT-Server-Private-IP-Address> ansible_ssh_user=ec2-user
<Web2-UAT-Server-Private-IP-Address> ansible_ssh_user=ec2-user
``` 


<img width="575" alt="UAT priv IP" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/db085db0-54df-4607-8e10-cb250e057d63">


##### Editing Ansible configuration file
In /etc/ansible/ansible.cfg file, we will uncomment `roles_path` string and provide a full path to our roles directory `roles_path` = `/home/ubuntu/ansible-config-artifact/roles` so Ansible could know where to find configured roles.


This will be done with a text editor such as `vi` text editor using the command `sudo vi /etc/ansible/ansible.cfg`


For guide on how to use the vi text editor click [here] (https://www.tutorialspoint.com/unix/unix-vi-editor.htm)


<img width="794" alt="roles_path" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3c13b465-3c8f-4568-86ae-bc95bc5ba11e">


##### Configuring `main.yml`
It is time to start adding some logic to the webserver role. Go into tasks directory, and within the `main.yml` file, start writing configuration tasks to do the following:


- Install and configure `Apache` (httpd service)
- Clone Tooling website from GitHub `https://github.com/<your-name>/tooling.git`.
- Ensure the tooling website code is deployed to /var/www/html on each of 2 UAT Web servers.
- Make sure `httpd` service is started


  All these will be executed with the following lines of code

```
  ---
- name: install apache
  become: true
  ansible.builtin.yum:
    name: "httpd"
    state: present

- name: install git
  become: true
  ansible.builtin.yum:
    name: "git"
    state: present

- name: clone a repo
  become: true
  ansible.builtin.git:
    repo: https://github.com/AndromedaIsComingg/tooling.git
    dest: /var/www/html
    force: yes

- name: copy html content to one level up
  become: true
  command: cp -r /var/www/html/html/ /var/www/

- name: Start service httpd, if not started
  become: true
  ansible.builtin.service:
    name: httpd
    state: started

- name: recursively remove /var/www/html/html/ directory
  become: true
  ansible.builtin.file:
    path: /var/www/html/html
    state: absent
```

## Reference 'Webserver' role

Within the `static-assignments` folder, create a new assignment file for uat-webservers `uat-webservers.yml`. This is where you will reference the role created earlier.

```
---
- hosts: uat-webservers
  roles:
     - webserver
```


<img width="580" alt="uat assignmnts" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/e4a8433a-c620-48a1-9720-8f9c56e605db">


Remember that the entry point to our ansible configuration is the `site.yml` file. Therefore, you need to refer your `uat-webservers.yml` role inside `site.yml` just like we did with with `common-del.yml` earlier on. So our `site.yml` file will be updated as below.


```
---
- hosts: all
- import_playbook: ../static-assignments/common.yml

- hosts: uat-webservers
- import_playbook: ../static-assignments/uat-webservers.yml

```

## Commit & Test

Commit your changes, create a Pull Request and merge them to master branch just like we did while installing and removing `wireshark` earlier, make sure webhook triggered two consequent Jenkins jobs(`ansible` and `save_artifacts`), they ran successfully and copied all the files to your Jenkins-Ansible server into /home/ubuntu/ansible-config-artifact/ directory.


<img width="1275" alt="UAT jenkins builds" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/31e2dc19-3eb2-4032-8ec7-7f158f7d751f">


let us also check if files have been updated in the directory `/home/ubuntu/ansible-config-artifact`


<img width="615" alt="files check 2" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3c42d5c9-5884-4fb4-bd50-c15edd436d6e">



Now run the playbook against your `uat` inventory with the following commands and see what happens.


```
cd /home/ubuntu/ansible-config-artifact

ansible-playbook -i inventory/uat.yml playbooks/site.yml
```

<img width="970" alt="uat installed" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/b2d9e253-435e-4a21-a0a5-2b2622aea90b">


Since we have qa successfull play, we should be able to see both of your UAT Web servers configured and you can try to reach them from our browser using:

Note: Please ensure that port 80 is permitted from the `inbound rules` of the security group of the UAT web servers (web1-UAT & web2-UAT). This is because by default Apache uses port 80.


`http://<Web1-UAT-Server-Public-IP-or-Public-DNS-Name>/index.php`

or


`http://<Web2-UAT-Server-Public-IP-or-Public-DNS-Name>/index.php`


<img width="1245" alt="home page" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/f1b1a785-4f0d-4cea-af3a-722045d9c5cc">


Seeing the web page above means that:

- `Jenkins` has successfully performed the job of Continuous Integration and Continuous Delivery
  1. By serving as a gateway between GitHub and our Server
  2. Copying artifacts from one job to another using the `Copy Artifact` plugin
  3. Storing the copied artifacts on our server.
 

- `Ansible` has successfully performed Automation and carried out the following
  1. Configured our servers and hosts in the iventory
  2. Configured a `playbook` file `site.yml` to refactor the static assignments `/static-assignments/common.yml` and `/static-assignments/uat-webservers.yml`
  3. Configured the static assignments `/static-assignments/uat-webservers.yml` to the role `/task/main.yml'

 Ansible performed the following actions: 
- Installed and configure Apache (httpd service).
- Cloned Tooling website from GitHub.
- Ensured the tooling website code is deployed to /var/www/html on each of 2 UAT Web servers.
- Made sure httpd service is started.


 ---------------------------------![Alt Text](https://cssbud.com/wp-content/uploads/2021/05/thanks-for-your-time.gif)---------------------------------------------













