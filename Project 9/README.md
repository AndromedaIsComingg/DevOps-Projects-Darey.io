# Implementing Wordpress website with LVM Storage Management.

## What is WordPress?
At its core, WordPress is the simplest, most popular way to create your own website or blog. In fact, WordPress powers over 43.3% of all the websites on the Internet. Yes – more than one in four websites that you visit are likely powered by WordPress.

On a slightly more technical level, WordPress is an open-source content management system licensed under GPLv2, which means that anyone can use or modify the WordPress software for free. A content management system is basically a tool that makes it easy to manage important aspects of your website – like content – without needing to know anything about programming.

The end result is that WordPress makes building a website accessible to anyone – even people who aren’t developers.



## What is LVM (logical volume management)?

Logical volume management (LVM) is a form of storage virtualization that offers system administrators a more flexible approach to managing disk storage space than traditional partitioning. This type of virtualization tool is located within the device-driver stack on the operating system. It works by chunking the physical volumes (PVs) into physical extents (PEs). The PEs are mapped onto logical extents (LEs) which are then pooled into volume groups (VGs). These groups are linked together into logical volumes (LVs) that act as virtual disk partitions and that can be managed as such by using LVM.

The goal of LVM is to facilitate managing the sometimes conflicting storage needs of multiple end users. Using the volume management approach, the administrator is not required to allocate all disk storage space at initial setup. Some can be held in reserve for later allocation. The sysadmin can use LVM to segment logically sequential data or combine partitions, increasing throughput and making it simpler to resize and move storage volumes as needed. Storage volumes may be defined for various user groups within the enterprise, and new storage can be added to a particular group when desired without requiring user files to be redistributed to make the most efficient use of space. When old drives are retired, the data they contain can be transitioned to new drives -- ideally without disrupting availability of service for end users.

**This project will be excecuted with a 3 Tier Architecture**
##### What Does Three-Tier Architecture Mean?


A three-tier architecture is a client-server architecture in which the functional process logic, data access, computer data storage and user interface are developed and maintained as independent modules on separate platforms.

The Three Tiers in a Three-Tier Architecture
##### Presentation Tier
Occupies the top level and displays information related to services commonly available on a web browser or web-based application in the form of a graphical user interface (GUI).

It constitutes the front-end layer of the application and the interface with which end-users will interact directly.

This tier is usually built on web development frameworks, such as CSS or JavaScript, and communicates with other tiers by sending results to the browser and other tiers in the network through API calls.

##### Application Tier
This tier — also called the middle tier, logic tier, business logic or logic tier — is pulled from the presentation tier.

It controls the application’s core functionality by performing detailed processing and is usually coded in programming languages, such as Python, Java, C++, .NET, etc.

##### Data Tier
Houses database servers where information is stored and retrieved.

Data in this tier is kept independent of application servers or business logic, and is managed and accessed with programs, such as MongoDB, Oracle, MySQL, and Microsoft SQL Server.


##### The 3 tier architecture concept is illustrated with the diagram below: 


![Screen Shot 2023-10-27 at 4 46 05 AM](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/ddca816e-23ea-4625-b002-93fcbadac762)


##### In this project, we will be showcasing **Three-tier Architecture** while also ensuring that the disks used to store files on the Linux servers are adequately partitioned and managed through programs such as `gdisk` anad `LVM` respectively. 


#### The prerequisites for the implementing Wordpress website with LVM Storage Management are as follows:

- Stable network connection
- How to create an EC2 Instance
- Access to the terminal
- A user account with sudo privileges
- Basic Unix command knowledge
- A Laptop or PC to serve as a client
- AWS EC2 instance running a Linux OS to serve as a Web server
- AWS EC2 instance running a Linux OS to serve as database (DB) server


## Implementing LVM on Linux servers (Web and Database servers)

##### Prepare a Web Server
Launch an EC2 instance that will serve as "Web Server"
For this we will be using the Redhat distribution of the Linux OS
For guide on how to create an EC2 instance and connect to one, please visit my earlier documentation [here](https://github.com/AndromedaIsComingg/Other-Projects/blob/main/Project%204/README.md)
But it is important to note that the user name for the **Redhat** distribution on terminal will be `ec2-user` instead of `ubuntu` which was used for the **Ubuntu** distribution.

Create 3 volumes in the same as your Web Server EC2, each of 10GB

![EC2storage vol DB](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/1fda82b8-5a81-49dd-9bc5-8a63af13642a)

##### After connecting to the ec2 instance from terminal, we will use the `lsblk` command to see a list of block devices that is attached to the server


![lsblk](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/c793cfb7-befc-48f6-9d45-a30288912b07)


##### Using the `gdisk` command to create partition
Now we will create a single partition on each of the added volumes using the following command `sudo gdisk /dev/<volume label>`
Note that the name of each block is to be replaced in place holder the in the command.

upon the first prompt, type 'n' to create a new partition and upon the last prompt, type 'w' to save the partition.


![gdisk](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/d3ead504-9ba6-432e-939d-f184ca32f093)


##### Checking for new blocks
Now we will reuse the `lsblk` command to check for all the volumes including the newly created blocks.

![lsblk partitnd](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/91ff051b-0624-4c63-8550-643e0043f50b)


##### Server Update
It is best practice to update the server.
This will be done using the `yum` package manager as this is the packet manager for RedHat and CentOS


![yum update](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/50c1648e-0ce4-4826-bbdd-32b5db2f63d3)


##### Installing `lvm` and chechking for available partitions
use the the`sudo yum install lvm2` command to install `lvm` and `sudo lvmdiskscan` to check for available partitions.


![lmv2 install](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/bdde2525-c1ba-49e8-a484-dc81cdf22913)

##### lvmdiskscan

![lvmdiskscan initial](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/74766a82-fd28-43df-8b57-cedcc8c57f89)


##### Marking physical volumes
Use the `pvcreate` utility to mark each of the 3 disks as physical volumes (PVs) is to be used by LVM
using the command `sudo pvcreate /dev/<volume label>`
please note that partition name is to be replaced in the place holder


![physical volumes](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/e1e2c151-46b3-4d12-a27e-2b3a15d7f3eb)



##### Verifying physical volumes

to verify the just created physical volumes, we will use the command `sudo pvs`


![sudo pvs](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/b7adac3c-86a9-442e-b48d-6436f4ed3adb)


##### Creating Group for volumes
Use the vgcreate utility to add all 3 physical volumes to a volume group(VG). Name the VG `webdata-vg` with the code `sudo vgcreate webdata-vg /dev/<volume label1> /dev/<volume label2> /dev/<volume label3>`
please note to replace the names of the partitions in the place holders.

![VG Create](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/66517e66-fe66-4a26-a8b4-ef233aa7a1ce)


##### Verifying VG
This is done to verify the created VG using the command `sudo vgs`

![sudo vgs](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/eb85d3d8-eb61-4349-b697-48176e2ca5c8)


##### Creating Logical Volumes
Use the `lvcreate` utility to create two logical volumes `apps-lv` (Use half of the PV size) and `logs-lv` 
**lv use the will use the remaining space of the PV size**
Note that apps-lv will be used to store data for thw website, while logs-lv will be used to stored data for logs.
This will be done using the comands
`sudo lvcreate -n apps-lv -L 14G webdata-vg`
`sudo lvcreate -n logs-lv -L 14G webdata-vg`


![logical volumes](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/0ee24d52-9e65-451f-8a3f-cde331170661)


##### Verifyinging Logical Volumes
To verify that logical volumes have been created, we will use the command `sudo lvs`


![logical vols verify](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/6aff1239-5228-4104-a76a-6982bfcaaef1)


##### Verifyinging The Entire Setup
To verify the entire setup, we will do so with the codes below

`sudo vgdisplay -v #view complete setup - VG, PV, and LV`

![setup verify](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/fc98d02d-dadb-4fad-9fb3-0e03732aca1c)


`sudo lsblk` 


![setup verify lsblk](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/018e7dcf-74a2-47d3-9815-44f1608dff4f)


##### Formating Logical Volumes
Use `mkfs.ext4` to format the logical volumes with ext4 file system.
This is done using the commands below
`sudo mkfs -t ext4 /dev/webdata-vg/apps-lv`
`sudo mkfs -t ext4 /dev/webdata-vg/logs-lv`

![Formatng logical vols](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/9584b17f-7f01-4043-85cf-29ae7e46287d)

##### Creating /var/www/html directory 
This directory is created to store website files using the `mkdir` command 
`sudo mkdir -p /var/www/html`
![html dir](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/c2248580-cfc5-4bb5-9bf8-8c0289a1a07d)



##### Creating /home/recovery/logs directory
This directory is created to store backup log data
`sudo mkdir -p /home/recovery/logs`
![logs dir](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/fac8dc00-24a9-4d3b-b246-fcd5b9897a8a)


##### Mount /var/www/html on apps-lv logical volume
using the command `sudo mount /dev/webdata-vg/apps-lv /var/www/html/`

![mount LV](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/f0dfff5a-ee66-4ea6-b938-408a387d7342)



##### Backing up files in the log directory
Use the rsync utility to backup all the files in the log directory /var/log into /home/recovery/logs
Note that this is required before mounting the file system.

This is done using the command `sudo rsync -av /var/log/. /home/recovery/logs/`

![backup](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/3c9d33f8-043c-4c35-93b1-47c5cac4bdbd)


##### Mount /var/log on logs-lv logical volume. 
It is important to know that all existing data on /var/log will be deleted, this is why the ealier backup is very important.
This is done with the command `sudo mount /dev/webdata-vg/logs-lv /var/log`

![remount](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/0d02fcf7-8cbe-478e-a146-b1339c59954f)


##### Restoring log files back into /var/log directory
This is done with the command `sudo rsync -av /home/recovery/logs/log/. /var/log`

![Restoring backup](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/5556393e-7df7-4165-adfd-1c04570b8e6c)


##### Update /etc/fstab file so that the mount configuration will persist after restart of the server
This is done using the  `UUID` of `/etc/fstab` file to update the device using the command `sudo blkid` to fetch the UUID.

![UUID](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/1990feeb-c172-42c5-9762-e75da4243b68)

The `/etc/fstab` file will be edited using the vi text editor, where the UUIDs  will be pasted without the leading and ending quotes using `sudo vi /etc/fstab`
Using the vi editor, we will to switch to insert mode by pressing key `i` afterwhich we will save and exit the vi editor with the comand `wq!`

![vi UUID](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/1bd59e4c-b439-42e2-9754-d5fde77db922)



##### Testing the configuration and reloadind the daemon
This is done with the commands:

`sudo mount -a`
`sudo systemctl daemon-reload`

![system reload](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/423f6340-bdbf-476c-8d78-6815b05cb019)

##### Verifying the setup
This is done by using the command `df -h`

![verify setup](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/e1645334-9ac9-4fdd-bb49-6860d913b32c)


## Installing wordpress and configuring to use MySQL Database

##### Preparing the Database server
For this, we will launch another Linux instance, `DB Server`, and we will be using the same flavour, `RedHat`.
Also, we will be repeating the same processes as in the `Web Server` instance, but instead of `apps-lv` we will create `db-lv` and mount it to `/db` instead of `/var/www/html/`.



