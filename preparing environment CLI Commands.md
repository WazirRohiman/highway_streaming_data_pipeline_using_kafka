Download Kafka
```
wget https://archive.apache.org/dist/kafka/2.8.0/kafka_2.12-2.8.0.tgz
```

Extract Kafka
```
tar -xzf kafka_2.12-2.8.0.tgz
```

Star MySQL server
```
start_mysql
```

Connect to MySQL server / save password
```
mysql --host=127.0.0.1 --port=3306 --user=root --password=*enter password*
```

Create a database called 'tolldata'
```
create database tolldata;
```

use the database and create a new table to store all the stream data coming from kafka
Each row is a record of when a vehicle has passed through a certain toll plaza along with its type and anonymized id
```
use tolldata;

create table livetolldata(timestamp datetime,vehicle_id int,vehicle_type char(15),toll_plaza_id smallint);
```

Disconnect from MySQL Server
```
exit
```

Install the python module kafka-python using the pip command.
```
python3 -m pip install kafka-python
```

Install the python module mysql-connector-python using the pip command.
This python module will help you to communicate with kafka server. It can used to send and receive messages from kafka.
```
python3 -m pip install mysql-connector-python 
```

---------------------------------------------
Start Zookeeper
```
bin/zookeeper-server-start.sh config/zookeeper.properties
```

Open a new terminal and start a kafka server
```
cd kafka_2.12-2.8.0
bin/kafka-server-start.sh config/server.properties
```

Open a new terminal and create a new topic
```
cd kafka_2.12-2.8.0
bin/kafka-topics.sh --create --topic toll --bootstrap-server localhost:9092
```

Use this toll traffic generator
```
https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0250EN-SkillsNetwork/labs/Final%20Assignment/toll_traffic_generator.py
```

Run the generator
```
python3 toll_traffic_generator.py
```

Use this streaming_data_reader.py once downloaded, modify python file
```
https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0250EN-SkillsNetwork/labs/Final%20Assignment/streaming_data_reader.py
```

Run streaming_data_reader.py
```
python3 streaming_data_reader.py
```

The streaming toll data would get stored in the table 'livetolldata'
Connect to the database to check if the data has been inserted correctly














