# Continuous Integration with Jenkins


##### `Jenkins` is an open-source automation server commonly used for building, testing, and deploying software. It facilitates the continuous integration and continuous delivery (CI/CD) of code by automating the building, testing, and deployment phases of the software development lifecycle. Jenkins supports the automation of repetitive tasks, allowing development teams to focus on writing code rather than manually managing the development process.

Key features of Jenkins include:

- Continuous Integration: Jenkins can automatically trigger builds whenever changes are pushed to a version control repository, ensuring that code changes are regularly integrated and tested.

- Extensibility: Jenkins has a large ecosystem of plugins that extend its functionality. These plugins cover a wide range of tools and technologies, making it adaptable to various development environments.

- Pipeline Support: Jenkins supports the definition of continuous delivery pipelines, allowing users to define and automate the entire build, test, and deployment process.

- Distributed Builds: Jenkins can distribute build and test tasks across multiple machines, which helps in parallelizing and speeding up the build process.

- Integration: Jenkins can integrate with various version control systems (e.g., Git, SVN), build tools, testing frameworks, and deployment tools.

Community Support: Being open-source, Jenkins has a large and active community of users and contributors. This community support includes forums, documentation, and a wealth of plugins.

** Jenkins is widely used in software development and has become a standard tool for implementing CI/CD practices in many organizations. ** 

In this project, we will be setting up a Jenkins server, configure a job to automatically deploy source codes changes from Git to an NFS server.


See schematic below:

![image](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/6fdc1db4-36aa-4976-bfa7-fbb1a41eeeea)



## EC2 instance
We will provision an EC2 instance (Ubuntu 20.04 LTS)


For knowledge of how to create an EC2 Instance and how to connect to it. For guide on this, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/Other-Projects/blob/main/Project%204/README.md)


<img width="1252" alt="Ubuntu 20 04 LTS" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/da2f5106-b5e1-4960-b460-52a9d5a06fea">


##### Enable Ports
By default Jenkins server uses TCP port 8080 - open it by creating a new Inbound Rule in your EC2 Security Group


<img width="1240" alt="ports" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/de57e916-7eff-4915-a3f6-82e02779d7d5">

##### Installing Java Development Kit (JDK)
This is done because Jenkins is a Java-based application and it is done with the command `sudo apt install default-jdk-headless`

<img width="574" alt="JDK" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/7d61195a-f528-42a3-b679-0aa49dbfba29">


##### Install Jenkins

This is done with the commands


`curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install -y jenkins`


<img width="688" alt="Jenkins install" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/2b41b5b4-e595-4d29-8fa0-a36c0b1e494f">


##### Make sure Jenkins is running
sudo systemctl status jenkins
<img width="669" alt="Jenkins Status" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3d784ef7-cc4c-4dae-8197-164db617158f">

##### Launching Jenkins on Web Browser
this is done with the public IP of the jenkins instance and specifying port 8080

<img width="989" alt="Jenkins web unlock" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/bfdb19bb-78cc-469e-83d3-e7e155559dbb">


##### Unlocking Jenkins
This is done using the `cat` command to grab the password from the `initialAdminPassword` file in the following directory `/var/lib/jenkins/secrets/initialAdminPassword`

<img width="589" alt="Jenkins passwrd" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/86c510f7-8ef9-433b-8056-1f6dcdf58de5">


##### Install suggested plugins

<img width="819" alt="Suggested plugins" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/2e5f02f4-f9cc-4835-842d-3fda91eb8bff">


<img width="991" alt="suggested plugins install" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3ac53e77-fb05-4e9d-a7b6-5b0a768e8c83">


##### Create User
Fill in blanks accordingly

<img width="986" alt="Create User" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/cb562689-edcd-4d87-8567-98fa6654ba5b">


<img width="759" alt="Jenkins is ready" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/fdd104e9-61c7-413c-965d-4444541ef8f8">


## Cinfiguring Jenkins to retrieve source codes from Github using Webhooks
In this part, we willl configure a simple Jenkins job/project. This job will be triggered by GitHub Webhook and will execute a `build` task to retrieve codes from Github and store it locally on Jenkins Server.

##### Enable Webhook 
This is done in the GitHub Repository Settings
<img width="1171" alt="webhook enable" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/eb9bb98b-62c0-4539-a467-16f414ca86b6">


Fill the `Paylaod URL` with `<jenkins-URL+port>/github-webhook/`, select "Content type" `application/jason'

<img width="861" alt="webhook payload content type" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/0207d61c-7a8c-4f15-8219-64712c278b74">


## Creating a Jenkins Project
From the Jenkins web consle, click "New item" "Create job" and create a "Freestyle project", For this, we are naming "project11"

<img width="992" alt="project name" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/a6e435fd-d07c-4ac5-87be-6d9664911a55">


Give the Job a name and under source `code management`, select `Git` and paste the repository URL

<img width="1023" alt="Github link" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/8ca9c69d-2ab5-448d-bdf9-64e74183ace6">


Add `Credentials`, Jenkins (user/password) so Jenkins could access files in the repository.

<img width="1181" alt="Credentials" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/7ddfc615-8aed-47f4-bd63-e4d67ae464d1">

## Build Test
Saving the above configuration takes us back to the dashboard where we will use the `Build Now` option to test the congiguration


If you see a green tick sign before #1 at the lower left side of the console, it means everything was configured correctly and the build was successfull.


<img width="1280" alt="build 1" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/448610d8-dfc4-4640-b6b5-b0c7b1536b76">


If you have an error which looks like `HTTP ERROR 403 No valid crumb was included in the request` 

Then go back to Dasboard, Manage Jenkins, Configure Global Security, scroll down and check "enable proxy compactibility"


## Configuring Github to trigger Build Jobs Automatically
We will do this by selecting the job (project11) then "configure", go to the "Build Triggers" tab, this is where we will check the option "GitHub hook trigger for GITsm polling"

<img width="780" alt="build trigger" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/9c8b3eb0-9901-4761-b186-4031cbc03f0b">




##### Configure "Post-build Actions" to archive all the files - files resulted from a build are called "artifacts".

Move to the "Build Environment" tab, click the "Add post-build action" dropdown and select "Archive the artifacts"


In the "Files to archive" blank bar, fill in `**` 

<img width="634" alt="files to archive" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/0622c27a-f08c-42ff-ac25-064989a8fd0b">


##### Checking if auto biuld configuration is effective
This is done by editing any content in the GitHub repository, for this we will choose the README markdown file, where we will add a few text and check to see if it triggers an auto build in Jenkins

<img width="1266" alt="editing README for trigger" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/13d8106a-c0af-47f6-a684-151871a271e3">


<img width="700" alt="Auto build jenkins" src="https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/233dd58c-75e9-4ffd-941e-f6c4cdaabcfb">

By default, the artifacts are stored on Jenkins server locally in the directory

`ls /var/lib/jenkins/jobs/<name-of-freestyle-project>/builds/<build_number>/archive/`



---------------------------------![Alt Text](https://cssbud.com/wp-content/uploads/2021/05/thanks-for-your-time.gif)---------------------------------------------

