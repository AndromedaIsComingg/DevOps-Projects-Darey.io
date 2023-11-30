# Ansible Refactoring & Static Assignments (Imports and Roles)


## Jenkins job enhancement

Before we begin, let us make some changes to our Jenkins job - now every new change in the codes creates a separate directory which is not very convenient when we want to run some commands from one place. Besides, it consumes space on Jenkins server with each subsequent change. Let us enhance it by introducing a new Jenkins project/job - we will require `Copy Artifact` plugin.


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


## Refactor Ansible code by importing other playbooks into `site.yml`

Let see code re-use in action by importing other playbooks.


Before starting to refactor the codes, ensure that you have pulled down the latest code from main branch, and create a new branch, name it `refactor`.


This will be done with the command `git checkout -b refactor`


<img width="799" alt="refactor" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/b1c82241-bf2f-43c5-82e2-40f522e82f8c">






