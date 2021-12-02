# Guacamole IMS for Flexible Engine

This document describe how to run a fully working **Apache Guacamole (incubating)** ECS instance build on docker (docker-compose) in Flexible Engine with SSH and RDP session pre configured all in a box.

Image is build on Ubuntu 20.04 with the following packages :

- docker 
- ubuntu desktop
- xrdp

## 

## About Guacamole

Apache Guacamole (incubating) is a clientless remote  desktop gateway. It supports standard protocols like VNC, RDP, and SSH.  It is called clientless because no plugins or client software are  required. Thanks to HTML5, once Guacamole is installed on a server, all  you need to access your desktops is a web browser.

It supports RDP, SSH, Telnet and VNC and is the fastest HTML5 gateway I know. Checkout the projects [homepage](https://guacamole.incubator.apache.org/) for more information.

## 

## Docker Compose

This image is based on the following project :

https://github.com/boschkundendienst/guacamole-docker-compose



## ECS configuration from IMS

From Image Management Service (IMS) :

- Go to Image share with me
  - Select : guacamole
- in Operation section choose : Apply for Server
- Configure the ECS with your preferred configuration
  - 1 vCPUs and 2GiB of RAM is enough to run the Remote Desktop
  - Assign an EIP if you are not using an ELB (10 Mbit/s is recommended)

Finally open TCP port 8443 and 4444 in your security group associated to the ECS

## 

## Accessing Guacamole

#### URL

Once your ECS is up and running, in your favorite browser go to :

https://x.x.x.x:8443

Replace x.x.x.x by the EIP assign to your ECS

#### Login

user / password is : 

guacadmin / guacadmin

### Guacamole Configuration

#### User configuration

I strongly recommend to create a new user :

In the top right menu (guacadmin)

- go to Settings
  - User
    - Create a new user with all right
- Log out
- Log in with your new user
  - in the user configuration deactivate the guacadmin account

#### SSH and RDP connections

In the Settings

- Connections
  - Edit the ssh-local template
    - replace the name  
    - the ip by yours ECS IP
    - the password
    - the private key
  - Save
  - Edit the rdp-local template
    - the ip by yours ECS IP
  - Save

User / password for SSH :

cloud:Passw0rd21!

You can also access it through SSH directly on port 4444

