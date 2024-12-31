# Kafka
This GitHub repository will include all Leverate DevOps-Team Kafka configurations.

# SECTION 1 - docker-composeSWARM.yml 

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

docker stack deploy -c docker-composeSwarm.yml kafka-cluster

# 3. Check the stack

docker stack ps <stack name>

For example  :

docker stack ps kafka-cluster


# Healthy state : 

ID             NAME                               IMAGE                              NODE            DESIRED STATE   CURRENT STATE               ERROR     PORTS
1hnyfwg5hp7t   kafka-cluster_kafdrop.1            obsidiandynamics/kafdrop:3.27.0    KafkaDocker-1   Running         Running about an hour ago
tqstpii8ipe0   kafka-cluster_kafka-broker-2.1     bitnami/kafka:latest               KafkaDocker-2   Running         Running about an hour ago
k4yhgw49xs2h   kafka-cluster_kafka-broker-3.1     bitnami/kafka:latest               KafkaDocker-3   Running         Running about an hour ago
ioq822kz4nay   kafka-cluster_kafka-controller.1   bitnami/kafka:latest               KafkaDocker-1   Running         Running about an hour ago
qyxpk4iaelnl   kafka-cluster_zookeeper.1          confluentinc/cp-zookeeper:latest   KafkaDocker-2   Running         Running about an hour ago

