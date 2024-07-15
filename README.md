# DevOps-Project-3tier-Application-Deployment-AKS-RabbitMQ-Memcache-MySQL8-Pod-based
![image](https://github.com/user-attachments/assets/5935dc09-0cf8-4f90-95e3-77b75b3d6a08)
![image](https://github.com/user-attachments/assets/c8eafd13-0fbb-4fd6-a5be-8641cc7a037d)

Architecture diagram for three-tier Application deployment and three-tier Application is as shown above.

I have used terraform script as provided in this repository to create the Azure VMs, Application Gateways, AKS and Azure Database for PostgreSQL Flexible Servers.

I have created RabbitMQ cluster with three kubernetes pods. Follow below procedures to achieve the same.

Create Azure DevOps pipeline for deployment of Tomcat Application Pods, RabbitMQ Pods, Memcached Pods and MySQL Pods using the azure-pipelines.yaml file prresent with this repository.
```
Add a user and permission to the user in RabbitMQ. Assign Role for High Availability (HA) using the commands as shown below.

rabbitmqctl add_user test test
rabbitmqctl set_user_tags test administrator
rabbitmqctl set_permissions -p / test ".*" ".*" ".*"
rabbitmqctl set_policy ha-all ".*" '{"ha-mode":"all","ha-sync-mode":"automatic"}' 
```
![image](https://github.com/user-attachments/assets/e4648891-b703-4efd-8bae-f76afd5b3256)

Create Ingress rule using the rabbitmq-ingress-rule.yaml file as present in this repository and do the entry in Azure dns-zone for Hosts corresponding to IP Address as shown below.
![image](https://github.com/user-attachments/assets/7dd2c517-e3a0-4a77-90c3-836cb8b72d82)
![image](https://github.com/user-attachments/assets/82c379f4-36ea-45b4-8e16-024433e87860)


