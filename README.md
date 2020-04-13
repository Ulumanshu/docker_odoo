# docker_odoo
Example template for odoo deployment with docker

## Install Docker

Latest version(not necessary):  
* [installing docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04)  
* [installing docker compose](https://docs.docker.com/compose/install/)  
Older version apt-get:  
* [installing docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04)
* `$ sudo apt-get install docker-compose`  

## General idea

Use docker-compose up command to blast launch prod and test odoo instaces and also the  
psql service instance. Also mount volumes so odoo internal maintenace modules can  
permanetly download content onto host machine and its possible to restart odoo service  
from interface.

## Challenges

* To fully incorporate the idea symlinks created inside the docker have to be transferred  
into odoo_addons folder somehow. Symlinks are being created by maintenance module when  
update is triggered from ui. Posibbly the module can be changed, but the point is to make  
as much as posible using docker and shell scripts.  

Solved:  
[Docker internal named volumes](https://devopsheaven.com/docker/docker-compose/volumes/2018/01/16/volumes-in-docker-compose.html)  

* Find a way to shut down docker from ui  

Solved:  
`$ service odoo restart` can be used inside of container

## Usefull Commands

* Start the docker stack psql and prod-test servers of odoo  
`$ sudo docker-compose up -d`  

* List running docker containers  
`$ sudo docker ps`  

![Alt text](src/img/containers.jpg?raw=true "Container List")

* Stop individual docker container (restarts with new settings when relaunched)  
`$ sudo docker stop docker_name`  

* Connect to container to execute some bash magick  
Main user:
`$ sudo docker exec -ti docker_name bash`  
Root:
`$ sudo docker exec -ti -u 0 docker_name bash`  

* Logging odoo service in docker container  
`$ sudo docker exec -ti docker_name bash`  
`$ tail -f 1000 /var/log/odoo/odoo.log`  

* Connecting to psql image in this conf and logging to databases  
`$ sudo docker exec -ti docker_name bash`  
`$ psql template1 odoo`  

## Easy instalation procedure on new server

`$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common gnupg`  
`$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`  
`$ sudo apt-key fingerprint 0EBFCD88`  
`$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`  
`$ sudo apt update`  
`$ sudo apt install docker-ce`  
`$ sudo usermod -aG docker $USER`  
`$ sudo apt-get install docker-compose`  
`$ git clone https://github.com/Ulumanshu/docker_odoo.git`  
`$ cd docker_odoo`  
`$ sudo docker-compose up -d`  

This is it you deployed everything and everything works. Go to http://hostname:8069  
test_maintenance modules in addon folder have to be replaced with your companys maintenance module

## Links

* [official odoo image](https://hub.docker.com/_/odoo)  


