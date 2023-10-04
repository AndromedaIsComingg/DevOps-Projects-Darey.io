# Implementing Loadbalancers with Nginx

What is load balancing?
Load balancing is the method of distributing network traffic equally across a pool of resources that support an application. Modern applications must process millions of users simultaneously and return the correct text, videos, images, and other data to each user in a fast and reliable manner. To handle such high volumes of traffic, most applications have many resource servers with duplicate data between them. A load balancer is a device that sits between the user and the server group and acts as an invisible facilitator, ensuring that all resource servers are used equally.

##### The concept is shown by the illustration below

<img width="861" alt="Introduction Image" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/8a6ea022-db0f-4241-9a09-48e45f816620">



Nginx is a versertile software, it can act like a web server, reverse proxy, and a load balancer. All that is needed is to configure it properly for which purpose.

##### The concept of using Nginx as a load balancer is shown by the illustration below


![nginx-as-load-balancer](https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/a296006e-1fd8-477b-9c6b-d281565f57cd)


#### The prerequisites for the implementation of Loadbalancers with Nginx on Linux are as follows:

- Stable network connection
- Basic Unix command knowledge
- A system running Linux or an AWS EC2 instance running a Linux OS
- Access to the terminal
- A user account with sudo privileges


