# docker_swarm

[ec2-user@manager ~]$ docker swarm init


#!/bin/bash

sudo yum install docker -y
sudo systemctl restart docker.service
sudo systemctl enable docker.service
sudo usermod -a -G docker ec2-user
sudo hostnamectl set-hostname worker2-ap-south-1.compute.internal
docker swarm join --token SWMTKN-1-2pcnaznflz6ej4n4o4bnsr49uasiez8rnxb903lzdwayf9j04e-a59vzthozqxzocmxn9iwvod04 172.31.47.219:2377


[ec2-user@manager ~]$ docker node ls
ID                            HOSTNAME                              STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
ywtgrao6u7u87gkkifkk0t0ua *   manager.ap-south-1.compute.internal   Ready     Active         Leader           20.10.17
nj5ykn24zl510k35bpc343jka     worker1-ap-south-1.compute.internal   Ready     Active                          20.10.17
w3d4etrqvadhyk9716p7vm9gk     worker2-ap-south-1.compute.internal   Ready     Active                          20.10.17
47srrzly7rygtg2d0xgniolvk     worker3-ap-south-1.compute.internal   Ready     Active                          20.10.17


