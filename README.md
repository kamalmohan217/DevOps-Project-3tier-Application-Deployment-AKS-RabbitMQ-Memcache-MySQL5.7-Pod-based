# DevOps-Project-3tier-Application-Deployment-AKS-RabbitMQ-Memcache-MySQL8-Pod-based
![image](https://github.com/user-attachments/assets/4a67b13c-de54-441f-b1a0-20c20ad859ed)

In the Architecture diagram shown above a basic architecture of three-tier application is shown. In this diagram the first layer or tier is Presentation Layer or web tier. The second layer or tier is Application Layer or Business Tier and third layer or tier is Database Layer or Database tier. For web tier Nginx Service, for Application tier Tomcat and for Database tier MySQL and Memcache(for cache purpose) has been used as shown in the Architecture diagram above.

![image](https://github.com/user-attachments/assets/c8eafd13-0fbb-4fd6-a5be-8641cc7a037d)
![image](https://github.com/user-attachments/assets/5935dc09-0cf8-4f90-95e3-77b75b3d6a08)

Architecture diagram for three-tier Application and three-tier Application deployment is as shown above.

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

![image](https://github.com/user-attachments/assets/34e243b3-985c-483d-bc8c-f3361d825f05)

The source code is present in Azure Repos. I have taken the Source Code present in GitHub Repository https://github.com/kamalmohan217/Three-tier-WebApplication.git and did changes in pom.xml, Dockerfile, application.properties as shown below.

![image](https://github.com/user-attachments/assets/20d8d1ac-b7c5-4ecd-850a-bc0ba766bfad)
![image](https://github.com/user-attachments/assets/c027ad1c-8a88-4f56-838c-659ce79465e8)
![image](https://github.com/user-attachments/assets/9ca4d1bb-0976-4293-841b-db7ba7b75917)
![image](https://github.com/user-attachments/assets/19fde3a2-a1e2-464f-95d7-621c0cc25509)

For Azure Artifacts, copy below section and paste to pom.xml as I have shown in above screenshot.

![image](https://github.com/user-attachments/assets/5b1b7103-e06b-49ca-8522-9da5c8484d08)
![image](https://github.com/user-attachments/assets/04b417a3-c738-4a7b-bab7-df23e16c471c)

Provide Contributor Access for Azure Artifacts as shown in screenshot below.

![image](https://github.com/user-attachments/assets/69d235a4-4d1d-4bcc-87d1-29c87629c5f2)
![image](https://github.com/user-attachments/assets/146adf49-5f7b-4f1f-a565-2a994e50561d)

I have created a mysql image and kept it in Docker Hub Repository. While creating mysql pod I imported the .sql extension file db_backup.sql. The Dockerfile to achieve this is as shown below.

![image](https://github.com/user-attachments/assets/0a7df3a3-2c4b-48c3-b85d-69275bc3635e)
In Dockerfile as shown above in the attached screen-shot, **docker-entrypoint-initdb.d** directory contains the shell-script and .sql extension file which will get executed when container will be created for the first time. You can consider it as for keeping the bootstraping script.
