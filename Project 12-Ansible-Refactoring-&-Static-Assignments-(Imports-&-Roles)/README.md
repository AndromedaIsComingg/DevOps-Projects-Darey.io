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





