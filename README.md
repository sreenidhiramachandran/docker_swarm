# docker_swarm


Docker is a tool used to automate the deployment of an application as a lightweight container so that the application can work efficiently in different environments.

Docker Swarm is a clustering and scheduling tool for Docker containers. 
Clustering is an important feature for container technology, because it creates a cooperative group of systems that can provide redundancy, enabling Docker Swarm failover if one or more nodes experience an outage. A Docker Swarm cluster also provides administrators and developers with the ability to add or subtract container iterations as computing demands change.

Here, we create an overlay network for our services. 

#### We are using one master and three worker nodes in this case.  

![image](https://user-images.githubusercontent.com/120683482/216436604-81ba1697-a144-42dc-a855-60ad1fa3ede3.png)

#### Initializing docker swarm
```
[ec2-user@manager ~]$ docker swarm init
```
![image](https://user-images.githubusercontent.com/120683482/216430526-74929358-a540-4795-852d-25ea7fb3bf6b.png)


#### Creating a custom bridge


![image](https://user-images.githubusercontent.com/120683482/216434371-8f00ad94-aca2-4ade-a128-4ed49716c0c6.png)

#### On the worker nodes, install docker and use the token obtained from the master node to join the cluster 
```
#!/bin/bash

sudo yum install docker -y
sudo systemctl restart docker.service
sudo systemctl enable docker.service
sudo usermod -a -G docker ec2-user
sudo hostnamectl set-hostname worker2-ap-south-1.compute.internal
docker swarm join --token SWMTKN-1-2pcnaznflz6ej4n4o4bnsr49uasiez8rnxb903lzdwayf9j04e-a59vzthozqxzocmxn9iwvod04 172.31.47.219:2377
```

After configuring the worker nodes, run the below commands from the master node to see the worker nodes added to the cluster
```
$ docker node ls
```

![image](https://user-images.githubusercontent.com/120683482/216430620-a681e073-4c11-4aa4-baf3-4ef8dcc6f4fb.png)

```
[ec2-user@manager ~]$ docker node update --availability drain manager.ap-south-1.compute.internal
```

Add labels,
```
[ec2-user@manager ~]$ docker node update --label-add service=api-service worker1-ap-south-1.compute.internal
```
![image](https://user-images.githubusercontent.com/120683482/216431118-13cffc5d-7f7a-4a28-86d4-ef3b658f6673.png)


To check if the labels are added correctly,
```
[ec2-user@manager ~]$ docker node inspect worker1-ap-south-1.compute.internal
```

redis cache

![image](https://user-images.githubusercontent.com/120683482/216431584-e444ecd2-624f-4179-ad69-576aeb64d5c0.png)


api

![image](https://user-images.githubusercontent.com/120683482/216434654-b474b76f-6ec3-4dc0-9239-3f5f65fc2f36.png)



frontend

![image](https://user-images.githubusercontent.com/120683482/216434809-abc6dd94-ed7f-450b-b1e5-4474d0d80297.png)


LB

![image](https://user-images.githubusercontent.com/120683482/216436117-c53fa739-8d27-41f7-a3f0-518fe63d2c06.png)


Output

![image](https://user-images.githubusercontent.com/120683482/216434953-d77f84b7-457d-46d6-89db-86d258dc0de2.png)



![image](https://user-images.githubusercontent.com/120683482/216435055-35b892cb-08a2-4a64-90fa-34eca7433840.png)



![image](https://user-images.githubusercontent.com/120683482/216435562-90d55d43-1f02-4760-a2a0-c68644e298c7.png)


![image](https://user-images.githubusercontent.com/120683482/216435730-1242fb27-8db5-4ad9-ae76-bae59f9a62de.png)

