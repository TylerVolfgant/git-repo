#Create Docker network and volumes:

docker network create monitoring
docker volume create grafana-volume 
docker volume create influxdb-volume

#Check status

docker network ls
docker volume ls

#Start docker-compose.yml from dir

docker-compose up -d

#Check status 

docker ls

#Create admin in your influxdb container

docker exec -it <container_id> /bin/bash

influx
> CREATE USER admin WITH PASSWORD 'Ww123456' WITH ALL PRIVILEGES

#Enable HTTP Authentication in your configuration file

sudo nano /etc/influxdb/influxdb.conf

#uncomment and make settings

[http]
  enabled = true
  bind-address = "0.0.0.0:8086"
  auth-enabled = true

#restart your container

docker container restart <container_id>

#Now work with telegraf

sudo useradd -rs /bin/false telegraf

sudo mkdir -p /etc/telegraf

#you can use my telegraf.conf file

#than resrart telegraf container

#check logs telegraf container

docker container logs -f telegraf

#You must see something like that

#I! Starting Telegraf 1.13.0
#I! Using config file: /etc/telegraf/telegraf.conf
