# APACHE KAFKA
-------------------

Apache Kafka® is a distributed event streaming platform that is used for building real-time data pipelines and streaming applications.. It was originally developed at LinkedIn and later on become part of Apache Project.<br>
Kafka is fast, reliable, scalable, durable, fault-tolerant and distributed by design.

## KAFKA TERMINOLOGIES
-------------------

**Topic** - A topic is a category or feed name to which records are published.
		Topic is an entity in Kafka with a name. <br/>
**Zookeper** - is used for managing and coordinating Kafka Broker. <br>
**Broker** - kafka cluster is a set of servers, each of which is called a broker. <br>
**Partition** - Topics are broken upto into ordered commit logs called partitions
			Partition is where the messages lives inside the topic. <br>
**Producer** - A producer can be any application who can publish message to a topic.<br>
**Consumer** - A consumer can be any application that subscribes to a topic and consumes the message. <br>

**Topic** <br><div>
 * a particular stream of data <br>
 * similar to a table in a database (without any constraints) <br>
 * you can have as many as topic you want <br>
 * a topic is identified by it's name <br>
 * topics can splits in partitions <br>

**Partitions** <br><div>
* Each partitions ia an ordered, immutable sequence of records <br>
* Each record is assigned a sequential number called **offet** <br>
* Each partitions are independent of each other <br>
* Ordering is guaranteed only at partition level <br>
* Partitions continuosly grows as new records are produced <br> </div>

 **Broker** <br><div>
 * a kafka cluster is composed of multiple brokers <br>
 * each broker is identified with it's ID (integer) <br>
 * each broker contains certain topics partitions <br>
 * after connecting to any broker (called bootstrap broker) you can connect to entire cluster <br><div>

 **Topic replication factor** <br><div>
 * topic should have replication factor > 1 <br>
 * the way if a broker is down, another broker can serve the data <br></div>

 **Concept of leader for a partition** <br><div>
 * at any time only 1 broker can be a leader for a given partition <br>
 * only that leader can receive and serve data for partition <br>
 * the other broker will synchronize the data <br>
 * there each partition has : one leader and multiple ISR (in-sync-replica) <br></div>

 **Producers** <br> <div>
 * Producers write data to topics. <br>
 * They only have to specify topic name and one broker to connect to, and kafka will automatically take care of 	 routing the data to the right brokers. <br></div>

 **Producers: Message keys** <br><div>
 * Producers can choose to send a key with the message <br>
 * If a key is sent, then the producer has the guarantee that all the messages for that key go to the same partition. <br>
 * This enables to guarantee ordering of the specific key. <br></div>

**Consumers** <br><div>
* Consumers read data from a topic <br>
* They only have to specify the topic name and one broker to connect to, and kafka will automatically take care of 
       pulling the data from the right brokers. <br></div>

**Consumer Group** <br><div>
 * Consumers read data in consumer groups <br>
 * Each consumer within a group reads from exclusive partitions <br>
 * You can't have more consumers than the partitions <br>
 * Kafka Broker manages the consumer groups, it acts as a group co-ordinator <br></div>

 **Consumer Offset** <br><div>
  * Behave like a bookmark for the consumer to start reading the messages from the point it let off. <br></div>

## Why is Kafka so fast?

Kafka is known for its high performance and speed due to several reasons:

The two most important reasons are its low latency message delivery through **Sequential I/O** and **Zero Copy Principle**.

### Sequential IO :

Kafka relies heavily on the filesystem for storing and caching messages. The general perception is that "disks are slow, "meaning high seek time. Imagine if we can avoid seeking time. We can achieve low latency as low as RAM here. Kafka does this through Sequential I/O. Kafka efficiently uses log, an append-only, totally ordered data structure.

Traditional Data Transfer :

To read a file from a disk, then send it over the network, a traditional data transfer would require four context switches between user and kernel modes, making the data copied four times.

1) The File. read() call makes the context switch from user mode to kernel mode, and the data copy is performed by the direct memory access (DMA) engine, which reads the file content from the disk and stores it into a kernel address space buffer (OS buffer);

2) Data is copied from the kernel space buffer into the user buffer(Application buffer), making the File.read() call return and the context to switch back to user mode

3) The Socket.send() call makes the context switch to kernel mode, and the third data copy is performed from the user buffer(application buffer) to the kernel buffer(socket Buffer) again

4) Finally, the DMA engine performs a fourth copy of the data, passing it from the kernel buffer (socket buffer) to the network interface controller (NIC) buffer to be sent over the network.

If the requested data is larger than the kernel buffer size, there will be even more copies between kernel and user spaces. Zero-copy optimisation reduces these redundant data copies.

### Zero Copy Principle :

A zero-copy optimisation consists of removing the second and third data copies, making the data transferred directly from the OS buffer to the nic buffer. Kafka uses this zero-copy principle by requesting the kernel to move the data to nic rather than via the application. Zero Copy is a shortcut to save multiple data copies between the application and kernel contexts. This approach brings down the time approximately 65%.

### What else?
Kafka uses many other techniques apart from the ones mentioned above to make systems much faster and more efficient:

### Message Compression: 

Kafka allows for message compression, which reduces messages' size and enables faster data transmission and processing.
Message Batching: Kafka can batch messages together, which reduces the overhead of individual message processing and improves throughput.

Overall, Kafka's speed results from its optimised architecture(sequential io, append-only log, Zero Copy), compression, batching, in-memory storage.

## KAFKA Commands
-------------------
### Start Zookeeper
```
zookeeper-server-start.bat ..\..\config\zookeeper.properties
```
### Start Kafka Server
```
kafka-server-start.bat ..\..\config\server.properties
```
### Create Kafka Topic
```
kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 4 --topic test-topic
```
### Start producing topic through producer console
#### Without Key :
```
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test-topic --from-beginning
```
#### With Key :
```
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test-topic --from-beginning -property "key.separator= - " --property "print.key=true"
```
### List of all broker in the cluster
```
kafka-console-consumer.bat --bootstrap-server localhost:9092,localhost:9093,localhost:9094 --topic library-events --from-beginning
```
### Publish to the Kafka Topic via Console
```
kafka-console-producer.bat --broker-list localhost:9092 --topic test-topic
```
### Get Details of all Topic in a server
```
kafka-topics --bootstrap-server localhost:9092 --list
```
### Get Details of Topic
```
kafka-topics.bat --zookeeper localhost:2181 --topic test-topic --describe
```
### Delete topic
```
kafka-topics.bat --zookeeper localhost:2181 --delete --topic test-topic
```
### Get details of the consumer offset
```
kafka-topics.bat --zookeeper localhost:2181 --list
kafka-topics.bat --describe --zookeeper localhost:2181 --topic test-topic-replicated
```
### Get details of the consumer group
```
kafka-consumer-groups.bat --bootstrap-server localhost:9092 --list
```
### Stop Zookeeper and Kafka
```
zookeeper-server-stop.bat
kafka-server-stop.bat
```

