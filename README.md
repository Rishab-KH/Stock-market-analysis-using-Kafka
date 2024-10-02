# Stock-market-analysis-using-Kafka
Analyze simulated real-time stock data using Kafka on AWS EC2 instance 

SSH to AWS EC2 instance on terminal using the .pem file ssh -i {"key_file_name.pem"} ec2-user@ec2-{public-ip}.compute-1.amazonaws.com 

Steps to install Kafka:
'''
wget https://downloads.apache.org/kafka/3.3.1/kafka_2.12-3.11.0.tgz # To download the compressed file to EC2 instance 
tar -xvf kafka_2.12-3.11.0.tgz # To decompress the file

-----------------------
java -version # To verify if the instance exist
sudo yum install java # Install Java for Kafka to EC2 instance
java -version
cd kafka_2.12-3.11.0

Start Zoo-keeper:
-------------------------------
bin/zookeeper-server-start.sh config/zookeeper.properties # Start zookeeper server

Open another window to start kafka
But first ssh to to your ec2 instance


Start Kafka-server:
----------------------------------------
Duplicate the session & enter in a new console --
export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M" # Change heap memory
cd kafka_2.12-3.11.0
bin/kafka-server-start.sh config/server.properties 

It is pointing to private server, change server.properties so that it can run in public IP, we can use your IP but the ACL rules needs to be changed accordingly

To do this , you can follow any of the 2 approaches shared belwo --
Do a "sudo nano config/server.properties" - change ADVERTISED_LISTENERS to public ip of the EC2 instance 


Create the topic:
-----------------------------
Duplicate the session & enter in a new console --
cd kafka_2.12-3.11.0 
bin/kafka-topics.sh --create --topic {name of topic} --bootstrap-server {Put the Public IP of your EC2 Instance:9092} --replication-factor 1 --partitions 1 # Create topic with the IP, note the partition used here is 1 for project purpose

Start Producer:
--------------------------
bin/kafka-console-producer.sh --topic {name of topic} --bootstrap-server {Put the Public IP of your EC2 Instance:9092} # Create producer with the IP

Start Consumer:
-------------------------
Duplicate the session & enter in a new console --
cd kafka_2.12-3.3.1
bin/kafka-console-consumer.sh --topic demo_testing2 --bootstrap-server {Put the Public IP of your EC2 Instance:9092} # Create consumer with the IP

'''

## Architecture

Architecture used in the project is as follows: 

<img width="831" alt="image" src="https://github.com/user-attachments/assets/89bf33f7-be97-46ee-8189-2535b0961d99">

## Technology used

- Programming Language - Python
- Amazon Web Service (AWS)
  - S3 (Simple Storage Service)
  - Athena
  - Glue Crawler
  - Glue Catalog
  - EC2
- Apache Kafka



