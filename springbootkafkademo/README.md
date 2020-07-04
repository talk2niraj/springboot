## Reference URL
https://dzone.com/articles/running-apache-kafka-on-windows-os


# Steps to start ZooKeeper
1. Go to your ZooKeeper config directory. For me its C:\zookeeper-3.4.7\conf

2. Rename file “zoo_sample.cfg” to “zoo.cfg”

3. Open zoo.cfg in any text editor, like Notepad; I prefer Notepad++.

4. Find and edit dataDir=/tmp/zookeeper to :\zookeeper-3.4.7\data  

5. Add an entry in the System Environment Variables as we did for Java.

a. Add ZOOKEEPER_HOME = C:\zookeeper-3.4.7 to the System Variables.

b. Edit the System Variable named “Path” and add ;%ZOOKEEPER_HOME%\bin; 

6. You can change the default Zookeeper port in zoo.cfg file (Default port 2181).

7. Run ZooKeeper by opening a new cmd and type zkserver.

# Set up Kafka
1. Go to your Kafka config directory. For me its C:\kafka_2.11-0.9.0.0\config

2. Edit the file “server.properties.”

3. Find and edit the line log.dirs=/tmp/kafka-logs” to “log.dir= C:\kafka_2.11-0.9.0.0\kafka-logs.

4. If your ZooKeeper is running on some other machine or cluster you can edit “zookeeper.connect:2181” to your custom IP and port. For this demo, we are using the same machine so there's no need to change. Also the Kafka port and broker.id are configurable in this file. Leave other settings as is.

5. Your Kafka will run on default port 9092 and connect to ZooKeeper’s default port, 2181.

# Steps to start Kafka
Important: Please ensure that your ZooKeeper instance is up and running before starting a Kafka server.

1. Go to your Kafka installation directory: C:\kafka_2.11-0.9.0.0\

2. Open a command prompt here by pressing Shift + right click and choose the “Open command window here” option).

3. Now type .\bin\windows\kafka-server-start.bat .\config\server.properties and press Enter.

# Command to create topic
1. Open a new command prompt in the location C:\kafka_2.11-0.9.0.0\bin\windows.

2. Type the following command and hit Enter:

kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

# Command to start local Kafka producer (optional for this project)
1. Open a new command prompt in the location C:\kafka_2.11-0.9.0.0\bin\windows

2. To start a producer type the following command:

kafka-console-producer.bat --broker-list localhost:9092 --topic test

# Command to start local Kafka consumer
1. Open a new command prompt in the location C:\kafka_2.11-0.9.0.0\bin\windows

2. To start a consumer type the following command:

=> Before kafka version 2.0 (<2.0):

kafka-console-consumer.bat --zookeeper localhost:2181 --topic test


=> After kafka version 2.0 (>= 2.0): 

kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test
