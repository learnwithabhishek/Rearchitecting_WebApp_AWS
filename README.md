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
![image](https://user-images.githubusercontent.com/110404399/230732588-07e75122-6267-4f90-a243-6c16bf459660.png)

Go to Amazon ElastiCache. Click Parameter groups, create parameter group
![image](https://user-images.githubusercontent.com/110404399/230732836-4879fd5b-ee5d-4021-9d2c-259a268f521c.png)

Go to subnet groups, create subnet group. 
![image](https://user-images.githubusercontent.com/110404399/230733005-633d398e-daff-47c5-b12c-cfff82233415.png)

Go to Memcached clusters, create memcached cluster
![image](https://user-images.githubusercontent.com/110404399/230733336-f0ffa0c6-212a-4b4d-a9d7-acf6171f7d14.png)

Go to Amazon MQ, click get started. Select broker engine type as rabbitmq. 
![image](https://user-images.githubusercontent.com/110404399/230733828-5b37091e-479b-44bf-9f14-f631f7801532.png)

To initialize the database we will create a temporary ec2 instance (mysql-client). Login to this instance and run following commands:

sudo apt update

sudo apt install mysql-client -y

mysql -h endpoint-of-rds-database -u username -psecretpassword

Edit security group of backend services to allow port 3306 from security group of mysql-client instance

git clone https://github.com/devopshydclub/vprofile-project.git

git checkout aws-Refactor

cd /vprofile-project/src/main/resources

mysql -h vprofile-rds-mysql.cahc53orze9y.us-east-1.rds.amazonaws.com -u admin -pW057hbCr23YUR329RW6c accounts < db_backup.sql

Go to Elastic Beanstalk, create application. 
![image](https://user-images.githubusercontent.com/110404399/230737602-0bd9e0f3-1ff3-46eb-8d1a-d45602227241.png)

beanstalk created 2 instaces for frontend application( in setting I mentioned minimum2 , maximum 8 instances)
![image](https://user-images.githubusercontent.com/110404399/230737673-3d325d87-a1b3-48f8-9a37-aeeb4bce2549.png)

Add all traffic allow from Security group of beanstalk in backend security group. Add listener https port 443;  healthcheck at /login ; ssl certificate in load balancer configuration of beanstalk.

Update application.properties file. Give rds database, Amazon MQ, elaticache endpoint dns
![image](https://user-images.githubusercontent.com/110404399/230738599-4d82af84-b4c1-4753-b37e-201c0bda0f35.png)

mvn clean install 

Go to beanstalk, application versions. Click on upload and select artifact created from mvn clean install.

![image](https://user-images.githubusercontent.com/110404399/230738878-29b4988f-af01-4c1e-a95c-2c456c7699cf.png)
![image](https://user-images.githubusercontent.com/110404399/230738901-0d1c8016-6baf-48f0-80a6-1f66b83bc419.png)

Select the application version and deploy 
![image](https://user-images.githubusercontent.com/110404399/230738990-3a96f72f-74a0-414e-b752-cb9d87cbc6a8.png)

Beanstalk update environment
![image](https://user-images.githubusercontent.com/110404399/230739108-d93dfca4-0d2d-4d64-b0e8-d69ef86bbf73.png)

After waiting for few minutes application deployed successfully
![image](https://user-images.githubusercontent.com/110404399/230739225-f64128d1-808d-40ef-89dc-42702615b43a.png)

In cloudfront create distribution
![image](https://user-images.githubusercontent.com/110404399/230739599-a56aa82e-99b0-4f75-8fc2-64a8ce72b0db.png)

![image](https://user-images.githubusercontent.com/110404399/230739988-e8bb5bdc-aeca-4f83-89fd-b03177a2427b.png)

Now we can access the application through cloudfront
![image](https://user-images.githubusercontent.com/110404399/230740049-644764a7-45cb-43d6-93e9-71caa0ce99dc.png)
