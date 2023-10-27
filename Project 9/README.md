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
- A Laptop and PC to serve as a client
- AWS EC2 instance running a Linux OS to serve as a Web server
- AWS EC2 instance running a Linux OS to serve as database (DB) server


## Implementing LVM on Linux servers (Web and Database servers)

##### Prepare a Web Server
Launch an EC2 instance that will serve as "Web Server"

Create 3 volumes in the same AZ as your Web Server EC2, each of 10GB
