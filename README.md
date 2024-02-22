# Stock Market Kafka Real Time

This project aims to create a real-time stock market monitoring system using Apache Kafka. It leverages Kafka's distributed streaming platform to process and analyze stock market data, providing insights into market trends and fluctuations.

## Architecture

![](Screenshots/Architecture.jpg)

## Technology Used
- Programming Language - Python
- Database - SQL
- Apache Kafka

Amazon Web Services (AWS)
1. EC2
2. S3
3. Glue
4. Crawlers
5. Athena

## Installation Steps:
- Download Kafka and Java:
```bash
wget https://downloads.apache.org/kafka/3.6.1/kafka_2.13-3.6.1.tgz
tar -xvf kafka_2.13-3.6.1.tgz

# Install Java
wget http://anduin.linuxfromscratch.org/BLFS/OpenJDK/OpenJDK-1.8.0.141/OpenJDK-1.8.0.141-x86_64-bin.tar.xz
tar -xvf OpenJDK-1.8.0.141-x86_64-bin.tar.xz

export JAVA_HOME=/home/ec2-user/OpenJDK-1.8.0.141-x86_64-bin

export PATH=$JAVA_HOME/bin:$PATH

echo 'export JAVA_HOME=/home/ec2-user/OpenJDK-1.8.0.141-x86_64-bin' >> ~/.bashrc

echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc

echo $JAVA_HOME

java -version

# To set the JAVA_HOME environment variable permanently on your Linux machine and add it to the PATH variable, you can follow these steps:

Determine the Java installation directory:

It seems like you have the OpenJDK directory OpenJDK-1.8.0.141-x86_64-bin.
You'll need the path to this directory to set the JAVA_HOME variable.
Edit the .bashrc file:

Open the .bashrc file located in your home directory using a text editor like nano or vim:

nano ~/.bashrc

Add the following lines at the end of the file to set the JAVA_HOME environment variable:
export JAVA_HOME=/path/to/your/java/directory/OpenJDK-1.8.0.141-x86_64-bin
export PATH=$PATH:$JAVA_HOME/bin

Replace /path/to/your/java/directory with the actual path to your Java installation directory.
Save the file and exit the text editor.

Source the .bashrc file to apply the changes to the current shell session:
source ~/.bashrc

Verify that the JAVA_HOME environment variable is set correctly:
echo $JAVA_HOME
This should display the path to your Java installation directory.

Verify that Java is correctly added to the PATH variable:
java -version
This command should display the version of Java installed on your system without any errors.


```
- Start Zookeeper:
``` bash 
cd kafka_2.12-3.3.1

bin/zookeeper-server-start.sh config/zookeeper.properties
```
- Start Kafka Server:
```bash
# In a new session
export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"

cd kafka_2.12-3.3.1

bin/kafka-server-start.sh config/server.properties
```
- Configure Server Properties:

To allow Kafka to run on a public IP, modify the server.properties file:
```bash
sudo nano config/server.properties

# Change ADVERTISED_LISTENERS to the public IP of the EC2 instance
```
- Create a Topic:
```bash
cd kafka_2.12-3.3.1

bin/kafka-topics.sh --create --topic kafka --bootstrap-server <aws ec2 public ip>:9092 --replication-factor 1 --partitions 1
```
- Start Producer:
```bash
bin/kafka-console-producer.sh --topic kafka --bootstrap-server <aws ec2 public ip>:9092
```
- Start Consumer:
```bash
# In a new session
cd kafka_2.12-3.3.1

bin/kafka-console-consumer.sh --topic kafka --bootstrap-server <aws ec2 public ip>:9092
```
- Install Kafka Python Library:
```bash
pip install kafka-python

pip install git+https://github.com/dpkp/kafka-python.git
```
- Search for Process ID and Kill:

To find and kill the Kafka and Zookeeper processes:
```bash
# For Zookeeper
sudo lsof -i :2181

# For Kafka Server
sudo lsof -i :9092

# Kill the process using PID
kill -9 <PID>
```

## Dataset Used
This dataset contains information about the Hang Seng Index (HSI) from 1986-12-31 to the present. Below is a brief description of the columns:

- Index: The stock market index representing the 50 largest companies listed on the Stock Exchange of Hong Kong.
- Date: The date of the trading session.
- Open: The opening price of the index.
- High: The highest price reached during the trading session.
- Low: The lowest price reached during the trading session.
- Close: The closing price of the index.
- Adj Close: The adjusted closing price of the index.
- Volume: The trading volume of the index.
- CloseUSD: The closing price of the index in US dollars.

The dataset provides insights into the daily trading performance of the Hang Seng Index, including price movements and trading volume. It can be used for various analytical purposes, including trend analysis, volatility assessment, and forecasting.


## References
1. Video tutorial - https://www.youtube.com/watch?v=KerNf0NANMo
2. AWS Account Tutorial - https://www.youtube.com/watch?v=kbtDJHgjrPc
3. Github project - https://github.com/darshilparmar/stock-market-kafka-data-engineering-project

