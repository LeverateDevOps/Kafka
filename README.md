# Kafka






This GitHub repository will include all Leverate DevOps-Team Kafka configurations.







# SECTION 1 - docker-composeSWARM.yaml 








# Prerequisites







In order to deploy this docker-compose file  we need to make sure of few things :

* Make sure all the Linux machines that will take part of the cluster can ping eachother by hostnames.
  
* Turn of sestatus and firewall.d on all machines.
  
* The Kafka-Controller will act as the Docker-Swarm manager

  

# 1. We will run the following command on the Kafka-Controller:









  
 docker swarm init --advertise-addr <MANAGER_IP>
  
- After running the init command, you will see  :
  
 docker swarm join --token SWMTKN-1-xxxxx <MANAGER_IP>:2377

 - We need to run the JOIN command on the WORKER nodes.


# 2. Deploy the stack 











docker stack deploy -c <docker compose file name> <stack name>

For example : 

docker stack deploy -c docker-composeSwarm.yaml kafka-cluster

# 3. Check the stack













docker stack ps <stack name>

For example  :

docker stack ps kafka-cluster









# SECTION 2  - docker-composeSINGLE.yaml








Since this configuration does not involve Docker-Swarm, and all Brokers and Controller are deploying on same machine -  we can easily deploy it with docker-compose.






# Deploy the docker-compose.yaml file 








* If no other docker-compose yaml file on your path we will run  -

  docker-compose up -d 

* If we want to specify the file -

  docker-compose -f docker-composeSINGLE.yaml up -d






# Check the cluster status 








docker ps 

docker ps -a # For all containers
