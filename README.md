# dataStreaming

#How To Install Docker Compose on Ubuntu 20.04
Now that we know what Docker Compose is, let's dive into installing the latest Docker Compose on Ubuntu. We'll borrow from the official Docker Compose Linux install docs, but we'll streamline the process here so you can hit the ground running with this demo project. Once Docker Compose is installed on our Ubuntu 20.04 system, we'll use it to run a simple multi-service demo app.

#Prerequisites
Access to the terminal of an Ubuntu 20.04 (or similar) system
sudo/root privileges
#Step 1: Add Docker's Repository To Your System
The recommended way to install Docker Compose and related packages from Docker is to add Docker's repository to your system's list of repos. Adding Docker's repo will allow you to download and update the latest packages using the apt package manager.

To begin, update your package list:<br>

```bash 
apt update -y
```
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2001-26-20.png"/>
Next, you'll need these four packages to allow apt to work with HTTPS-based repositories:

ca-certificates - A package that verifies SSL/TLS certificates.
curl - A popular data transfer tool that supports multiple protocols including HTTPS.
gnupg - An open source implementation of the Pretty Good Privacy (PGP) suite of cryptographic tools.
lsb-release - A utility for reporting Linux Standard Base (LSB) versions.
Use this command to install those packages:<br>

```bash 
apt install ca-certificates curl gnupg lsb-release
```
Output will look similar to:Install prerequisites

Make a directory for Docker's GPG key:<br>

```bash 
mkdir /etc/apt/demokeyrings
```
Use curl to download Docker's keyring and pipe it into gpg to create a GPG file so apt trusts Docker's repo:<br>

 ```bash 
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/demokeyrings/demodocker.gpg
```
 
Add the Docker repo to your system with this command:<br>
```bash 
 echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/demokeyrings/demodocker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list
```
The output should look similar to:Add official Docker repo<br>

#Step 2: Install Docker Compose And Related Packages<br>
Now that you added Docker's repo, update your package lists again:<be>

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2001-27-18.png"/>

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2001-30-46.png"/>



Next, install Docker-CE (Community Edition), the Docker-CE CLI, the containerd runtime, and Docker Compose with this command:<br>

```bash
apt update -y
```

```bash 
apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
Output should look similar to:Install Docker

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2001-31-20.png"/>
You can verify Docker-CE, the Docker-CE CLI, containerd, and Docker Compose are installed by checking their versions with these commands:<br>

```bash 
docker --version; docker compose version;ctr version
```

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2001-31-43.png"/>






Apache Nifi comes to mind if you are looking for a simple, but robust, tool to process data from various sources. 
In short, Apache NiFi is a tool to process and distribute data. Its intuitive UI supports routing definitions, a variety of connectors 
(in/out), and many built-in processors. All these features combined together make it a suitable optional platform for our use case.

#how to run nifi on ec2
```bash
https://hub.docker.com/r/apache/nifi/
```


https://hub.docker.com/r/apache/nifi-...

Step -1: Pull docker Image

```bash 
docker pull apache/nifi:latest
```

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-04%2001-08-23.png"/>

Step 2: Create a container

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-04%2001-22-17.png?token=GHSAT0AAAAAACF4RWELY5HNSKB5JV2MEVJMZGMDPOQ"/>

Name my container (I named it devnifi)

Controlling the port, and mapped to 8443

Being able to see the loading and standard output of Nifi

Create a shared volume between my host (shared-directory) and the container (ls-target)

```bash 
docker run --name devnifi -p 8081:8081 -d -e NIFI_WEB_HTTP_PORT='8081' apache/nifi:latest
```


Step 3: Verify using logs

```bash 
docker logs -f devnifi
```

Step 4: Pull Nifi registry and create container 

```bash 
docker pull apache/nifi-registry
```

then run the registry which managing version control for Nifi flow.

```bash 
docker run --name nifi-registry -p 18080:18080 -d apache/nifi-registr
```

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-04%2001-29-01.png?token=GHSAT0AAAAAACF4RWEKIDPNLURUGSABYGWEZGMDWIQ"/>

Step 5: Validation

visit
```bash 
http://publicIP:8081/nifi
```
 ```bash
http://publicIP:18080/nifi-registry
```

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-04%2001-30-57.png?token=GHSAT0AAAAAACF4RWEK7IAE45RY7ZBJFUFIZGMDUVA"/>

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-04%2001-30-45.png?token=GHSAT0AAAAAACF4RWEKH5BTZPKZT277UFEEZGMDUUQ"/>

#how to import template to nifi
      go to ```http://publicIP:8081/nifi```
      Download template Joshua-final-stocks-nifi.xml from this repo
      click upload template 
      select template and upload it.
      
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-04%2002-23-55.png?token=GHSAT0AAAAAACF4RWEKMU7ZNBHUJYEJOUBYZGMFGUQ"/>


# Aurora (MySQL Compatible)  

To create an Aurora DB cluster using the console
Sign in to the AWS Management Console and open the Amazon RDS console at https://console.aws.amazon.com/rds/.

In the upper-right corner of the AWS Management Console, choose the AWS Region in which you want to create the DB cluster.

Aurora is not available in all AWS Regions. For a list of AWS Regions where Aurora is available, see Region availability.

In the navigation pane, choose Databases.

Choose Create database.

For Choose a database creation method, choose Standard create.

For Engine type, choose one of the following:

Aurora (MySQL Compatible)

Aurora (PostgreSQL Compatible)


                                
                            
Choose the Engine version.

For more information, see Amazon Aurora versions. You can use the filters to choose versions that are compatible with features that you want, such as Aurora Serverless v2. For more information, see Using Aurora Serverless v2.

In Templates, choose the template that matches your use case.

To enter your master password, do the following:

In the Settings section, expand Credential Settings.

Clear the Auto generate a password check box.

(Optional) Change the Master username value and enter the same password in Master password and Confirm password.

By default, the new DB instance uses an automatically generated password for the master user.

In the Connectivity section under VPC security group (firewall), if you select Create new, a VPC security group is created with an inbound rule that allows your local computer's IP address to access the database.

For Cluster storage configuration, choose either Aurora I/O-Optimized or Aurora Standard. For more information, see Storage configurations for Amazon Aurora DB clusters.
                        
(Optional) Set up a connection to a compute resource for this DB cluster.

You can configure connectivity between an Amazon EC2 instance and the new DB cluster during DB cluster creation. For more information, see Configure automatic network connectivity with an EC2 instance.

For the remaining sections, specify your DB cluster settings. For information about each setting, see Settings for Aurora DB clusters.

Choose Create database.

If you chose to use an automatically generated password, the View credential details button appears on the Databases page.

To view the master user name and password for the DB cluster, choose View credential details.

To connect to the DB instance as the master user, use the user name and password that appear.

Important
You can't view the master user password again. If you don't record it, you might have to change it. If you need to change the master user password after the DB instance is available, you can modify the DB instance to do so. For more information about modifying a DB instance, see Modifying an Amazon Aurora DB cluster.

For Databases, choose the name of the new Aurora DB cluster.

On the RDS console, the details for new DB cluster appear. The DB cluster and its DB instance have a status of creating until the DB cluster is ready to use.


                        
                    
When the state changes to available for both, you can connect to the DB cluster. Depending on the DB instance class and the amount of storage, it can take up to 20 minutes before the new DB cluster is available.

To view the newly created cluster, choose Databases from the navigation pane in the Amazon RDS console. Then choose the DB cluster to show the DB cluster details. For more information, see Viewing an Amazon Aurora DB cluster.

                    
On the Connectivity & security tab, note the port and the endpoint of the writer DB instance. Use the endpoint and port of the cluster in your JDBC and ODBC connection strings for any application that performs write or read operations.










# Create a Database
To create a database in MySQL, execute the “CREATE DATABASE stream_db;” command:

CREATE DATABASE stream_db;


<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-04%2002-09-32.png?token=GHSAT0AAAAAACF4RWEKU7Q4PSMD5BR34BKWZGMFAHA"/>





#Running Apache Airflow container on ec2

Older versions of docker-compose do not support all the features required by the Airflow docker-compose.yaml file, so double check that your version meets the minimum version requirements.

The default amount of memory available for Docker on macOS is often not enough to get Airflow up and running. If enough memory is not allocated, it might lead to the webserver continuously restarting. You should allocate at least 4GB memory for the Docker Engine (ideally 8GB).

You can check if you have enough memory by running this command:

```bash 
docker run --rm "debian:bullseye-slim" bash -c 'numfmt --to iec $(echo $(($(getconf _PHYS_PAGES) * $(getconf PAGE_SIZE))))'
```

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2001-47-56.png"/>

Fetching docker-compose.yaml
To deploy Airflow on Docker Compose, you should fetch docker-compose.yaml.
```bash 
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.6.3/docker-compose.yaml'
```

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2001-51-06.png"/>

Initializing Environment
Before starting Airflow for the first time, you need to prepare your environment, i.e. create the necessary files, directories and initialize the database.

Setting the right Airflow user
On Linux, the quick-start needs to know your host user id and needs to have group id set to 0. Otherwise the files created in dags, logs and plugins will be created with root user ownership. You have to make sure to configure them for the docker-compose:


```bash
mkdir -p ./dags ./logs ./plugins ./config
```

```bash 
echo -e "AIRFLOW_UID=$(id -u)" > .env
```

For other operating systems, you may get a warning that AIRFLOW_UID is not set, but you can safely ignore it. You can also manually create an .env file in the same folder as docker-compose.yaml with this content to get rid of the warning:

```bash 
AIRFLOW_UID=50000
```

Initialize the database
On all operating systems, you need to run database migrations and create the first user account. To do this, run.

```bash 
docker compose up airflow-init
```

Running Airflow
Now you can start all services:

```bash
docker compose up
```

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2001-58-19.png"/>

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2002-28-55.png"/>
see the documentation:

https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html


#How to deploy fastapi using nginx

clone the repo by using this command
```bash 
git clone https://github.com/devhusnain/dataStreaming.git
```
use these commands to install python-pip and requirements for fastapi 
```bash 
sudo apt-get update
```
```bash 
sudo apt install python3-pip
```

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2001-56-07.png"/>


```bash 
pip3 install -r requirements.txt
```

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2002-01-00.png"/>

```bash 
sudo apt install nginx
```

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2002-06-47.png"/>



```bash
cd /etc/nginx/sites-enabled/
```


```bash
sudo nano fastapi_nginx
```

note: please change the public ip to ur ip
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2002-08-47.png"/>


```bash
 sudo service nginx restart
```
cd path to your fastapi


```python 
python3 -m uvicorn api:app
```

You can now access you fastapi via public ip 
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%20from%202023-08-06%2002-36-19.png"/>


# MSK service for kafka

From the Debezium website ``` https://debezium.io/releases/2.3/ ```, I download the MySQL connector plugin for the latest stable release. Because MSK Connect accepts custom plugins in ZIP or JAR format, I convert the downloaded archive to ZIP format and keep the JARs files in the main directory:

``` json
tar xzf debezium-connector-mysql-2.3.3.Final-plugin.tar.gz
```

```json
cd debezium-connector-mysql
```
```json
zip -9 ../debezium-connector-mysql-2.3.3.zip *
```
```json
cd ..
```

you can manully download this file  debezium-connector-mysql-2.3.3.Final-plugin.tar.gz  and create the zip file from it.



Then, upload the custom plugin to an Amazon Simple Storage Service (Amazon S3) bucket in the same AWS Region I am using for MSK Connect:
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/s3zip.png"/> 


<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/mskcluster1.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/mskcluster2.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/mskcluster3.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/mskcluster4.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/mskcluster5.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/mskcluster6.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/mskcluster7.png"/>



On the Amazon MSK console there is a new MSK Connect section. I look at the connectors and choose Create connector. Then, I create a custom plugin and browse my S3 buckets to select the custom plugin ZIP file I uploaded before.



I enter a name and a description for the plugin and then choose Next.



Now that the configuration of the custom plugin is complete, I start the creation of the connector. I enter a name and a description for the connector.



I have the option to use a self-managed Apache Kafka cluster or one that is managed by MSK. I select one of my MSK cluster that is configured to use IAM authentication. The MSK cluster I select is in the same virtual private cloud (VPC) as my Aurora database. To connect, the MSK cluster and Aurora database use the default security group for the VPC. For simplicity, I use a cluster configuration with auto.create.topics.enable set to true.






# Msk connector










```json
cat >>  ~/.bash_profile
export PATH=~/kafka_2.12-2.8.1/bin:$PATH                                        
export CLASSPATH=/home/ubuntu/aws-msk-iam-auth-1.1.9-all.jar
export BOOTSTRAP_SERVERS=b-1.msk.ciosr2.c2.kafka.us-east-1.amazonaws.com:9098,b-2.msk.ciosr2.c2.kafka.us-east-1.amazonaws.com:9098,b-3.msk.ciosr2.c2.kafka.us-east-1.amazonaws.com:9098
```

```json

connector.class=io.debezium.connector.mysql.MySqlConnector
database.history.producer.sasl.mechanism=AWS_MSK_IAM
database.history.producer.sasl.jaas.config=software.amazon.msk.auth.iam.IAMLoginModule required;
database.user=admin
database.server.id=123456
tasks.max=1
database.history.consumer.sasl.jaas.config=software.amazon.msk.auth.iam.IAMLoginModule required;
database.history.producer.security.protocol=SASL_SSL
database.history.kafka.topic=dbhistory.stream_db
database.history.kafka.bootstrap.servers=b-1.msk.ciosr2.c2.kafka.us-east-1.amazonaws.com:9098,b-2.msk.ciosr2.c2.kafka.us-east-1.amazonaws.com:9098,b-3.msk.ciosr2.c2.kafka.us-east-1.amazonaws.com:9098
database.server.name=stock-server
database.history.producer.sasl.client.callback.handler.class=software.amazon.msk.auth.iam.IAMClientCallbackHandler
schema.history.internal.kafka.bootstrap.servers=b-1.msk.ciosr2.c2.kafka.us-east-1.amazonaws.com:9098,b-2.msk.ciosr2.c2.kafka.us-east-1.amazonaws.com:9098,b-3.msk.ciosr2.c2.kafka.us-east-1.amazonaws.com:9098
database.history.consumer.sasl.client.callback.handler.class=software.amazon.msk.auth.iam.IAMClientCallbackHandler
database.history.consumer.security.protocol=SASL_SSL
database.port=3306
include.schema.changes=true
topic.prefix=stream_db_
schema.history.internal.kafka.topic=stream_db_internal
database.hostname=database-2-instance-1.cvyohyithmox.us-east-1.rds.amazonaws.com
database.password=12345678
database.history.consumer.sasl.mechanism=AWS_MSK_IAM
database.include.list=stream_db

```
Some of these settings are generic and should be specified for any connector. For example:

connector.class is the Java class of the connector.
tasks.max is the maximum number of tasks that should be created for this connector.
Other settings are specific to the Debezium MySQL connector:

The database.hostname contains the writer instance endpoint of my Aurora database.
The database.server.name is a logical name of the database server. It is used for the names of the Kafka topics created by Debezium.
The database.include.list contains the list of databases hosted by the specified server.
The database.history.kafka.topic is a Kafka topic used internally by Debezium to track database schema changes.
The database.history.kafka.bootstrap.servers contains the bootstrap servers of the MSK cluster.
The final eight lines (database.history.consumer.* and database.history.producer.*) enable IAM authentication to access the database history topic.

In Connector capacity, I can choose between autoscaled or provisioned capacity. For this setup, I choose provisioned and leave all other settings at their defaults.

For Worker configuration, you can use the default one provided by Amazon MSK or provide your own configuration. In my setup, I use the default one.

In Access permissions, I create a IAM role. In the trusted entities, I add kafkaconnect.amazonaws.com to allow MSK Connect to assume the role.

The role is used by MSK Connect to interact with the MSK cluster and other AWS services. For my setup, I add:

Permissions to write logs to a Amazon CloudWatch log group I created earlier.
Permissions to authenticate to my MSK cluster through IAM.
The Debezium connector needs access to the cluster configuration to find the replication factor to use to create the history topic. For this reason, I add to the permissions policy the kafka-cluster:DescribeClusterDynamicConfiguration action (equivalent Apache Kafka’s DESCRIBE_CONFIGS cluster ACL).

Depending on your configuration, you might need to add more permissions to the role (for example, in case the connector needs access to other AWS resources such as an S3 bucket). If that is the case, you should add permissions before creating the connector.

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/connector1.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/connector2.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/connector3.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/connector4.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/connector5.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/connector6.png"/>
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/connector7.png"/>




I download a binary distribution of Apache Kafka and extract the archive in the home directory:

$ tar xvf kafka_2.13-2.7.1.tgz
To use IAM to authenticate with the MSK cluster, I follow the instructions in the Amazon MSK Developer Guide to configure clients for IAM access control. I download the latest stable release of the Amazon MSK Library for IAM:

```json
wget https://github.com/aws/aws-msk-iam-auth/releases/download/1.1.0/aws-msk-iam-auth-1.1.0-all.jar
```
In the ~/kafka_2.13-2.7.1/config/ directory I create a client-config.properties file to configure a Kafka client to use IAM authentication:

```json
# Sets up TLS for encryption and SASL for authN.
security.protocol = SASL_SSL

# Identifies the SASL mechanism to use.
sasl.mechanism = AWS_MSK_IAM

# Binds SASL client implementation.
sasl.jaas.config = software.amazon.msk.auth.iam.IAMLoginModule required;

# Encapsulates constructing a SigV4 signature based on extracted credentials.
# The SASL client bound by "sasl.jaas.config" invokes this class.
sasl.client.callback.handler.class = software.amazon.msk.auth.iam.IAMClientCallbackHandler
```






In the third terminal connection, I install a MySQL client using the MariaDB package and connect to the Aurora database:

```json
$ sudo apt install mariadb
$ mysql -h database-2-instance-1.cvyohyithmox.us-east-1.rds.amazonaws.com -u admin -p

```

From this connection, I create the stock-database and a table for my stock:

```
CREATE TABLE stock (
    record_id INT NOT NULL AUTO_INCREMENT,
    time DATETIME NOT NULL,
    open FLOAT NOT NULL,
    high FLOAT NOT NULL,
    low FLOAT NOT NULL,
    close FLOAT NOT NULL,
    volume FLOAT NOT NULL,
    symbol VARCHAR(40),
    event_time DATETIME DEFAULT NOW(),
    PRIMARY KEY (record_id)
);
```


These database changes are captured by the Debezium connector managed by MSK Connect and are streamed to the MSK cluster. In the first terminal, consuming the topic with schema changes, I see the information on the creation of database and table:

# EMR
Create cluster  by clicking on button create cluster

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/Screenshot%202023-09-07%20202230.png" />
Choose name for the emr cluster and version i am using 6.9.0 version

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/1.png" />

Choose 3 Applications  Hive , Spark , Livy and choose aws glue data catalog settings  select use for spark table metadata

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/2.png" />

Choose primary , core and task instance  type i am using small
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/3.png" />

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/4.png" />

Select cluster size manually

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/5.png" />

choose vps of your choice

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/6.png" />

choose cluster termination 

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/7.png" />
choose your logs s3 bucket

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/8.png" />

Select ssh key
<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/9.png" />

create a service role or choose existing one i am select create a service role

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/10.png" />
Select ec2 role

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/11.png" />

Emr created wait for it to be available

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/12.png" />

Copy livy url from emr and paste there as shown in blow in in file lambda_function.py

<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/13.png" />

Copy livy url from emr and paste there as shown in blow in in file airflowlambda.py


<img src="https://raw.githubusercontent.com/devhusnain/dataStreaming/main/images/14.png" />


