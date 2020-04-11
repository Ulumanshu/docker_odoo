# docker_odoo
Example template for odoo deployment with docker

## Install Docker
Find ze best way to install now it is pretty complicated

## General idea
Use docker-compose up command to blast launch prod and test odoo instaces and also the  
psql service instance. Also mount volumes so odoo internal maintenace modules can  
permanetly download content onto host machine and its possible to restart odoo service  
from interface.

## Usefull Commands

Start the docker stack psql and prod-test servers of odoo
`$ sudo docker-compose up -d`

List running docker containers
`$ sudo docker ps`

![Alt text](src/img/containers.jpg?raw=true "Container List")

Stop individual docker container (restarts with new settings)
`$ sudo docker stop docker_name`

Connect to container to execute some bash magick
`$ sudo docker exec -ti docker_name bash`

Logging odoo service in docker container
`$ sudo docker exec -ti docker_name bash`
`$ tail -f 1000 /var/log/odoo/odoo.log`

Connecting to psql image in this conf and logging to databases
`$ sudo docker exec -ti docker_name bash`
`$ psql template1 odoo`



