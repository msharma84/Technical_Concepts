# APACHE KAFKA
-------------------

Apache Kafka is a distributed publish-subscribe messaging system. It was originally developed at LinkedIn and later on become part of Apache Project.
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
 * each partitions is ordered <br>
 * each message within a partition gets an incremental id, called an offset <br> </div>

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
