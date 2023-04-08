In this project we will use : 

Beanstalk: For hosting java web application

S3: for storage

RDS: for Mysql database

Elasticache: For caching service

ActiveMQ: For message broker

Route53: For DNS

CloudFront: For Content delivery accross the world

# Steps

Create a key pair
![image](https://user-images.githubusercontent.com/110404399/230730712-695de46c-5901-46f4-978b-b87232da9a5f.png)

Create a security group for backend services 
![image](https://user-images.githubusercontent.com/110404399/230731119-d2b197eb-b6e6-4f5e-9aed-ea5784e1265f.png)

Go to Amazon RDS, create subnet group
![image](https://user-images.githubusercontent.com/110404399/230731327-0cfc751c-a0c6-4f34-81cb-72e3848d8b11.png)
![image](https://user-images.githubusercontent.com/110404399/230731358-e638b5f6-8dd7-4b58-94bd-c6e8b4997bb5.png)

Go to parameter groups, create parameter group
![image](https://user-images.githubusercontent.com/110404399/230731528-98be8da2-1cdd-4d7c-b446-03c661e5c940.png)

Go to Databases, create database. Choose a database creation method as standard create. Engine option Mysql.

