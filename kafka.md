APACHE KAFKA
--------------

Apache Kafka is a distributed publish-subscribe messaging system. It was originally developed at LinkedIn and later on become part of Apache Project.
Kafka is fast, reliable, scalable, durable, fault-tolerant and distributed by design.

KAFKA TERMINOLOGIES
-------------------

**Topic** - A topic is a category or feed name to which records are published.
		Topic is an entity in Kafka with a name. <br>
**Zookeper** - is used for managing and coordinating Kafka Broker
**Broker** - kafka cluster is a set of servers, each of which is called a broker
**Partition** - Topics are broken upto into ordered commit logs called partitions
			Partition is where the messages lives inside the topic
**Producer** - A producer can be any application who can publish message to a topic
**Consumer** - A consumer can be any application that subscribes to a topic and consumes the message.

**Topic**
	- * a particular stream of data
	- * similar to a table in a database (without any constraints)
	- * you can have as many as topic you want
	- * a topic is identified by it's name
	- * topics can splits in partitions
	- * each partitions is ordered
	- * each message within a partition gets an incremental id, called an offset

 Broker
	* a kafka cluster is composed of multiple brokers
	* each broker is identified with it's ID (integer)
	* each broker contains certain topics partitions
	* after connecting to any broker (called bootstrap broker) you can connect to entire cluster

 Topic replication factor
	* topic should have replication factor > 1 
	* the way if a broker is down, another broker can serve the data

 Concept of leader for a partition
	* at any time only 1 broker can be a leader for a given partition
	* only that leader can receive and serve data for partition
	* the other broker will synchronize the data
	* there each partition has : one leader and multiple ISR (in-sync-replica)

 Producers
	* Producers write data to topics.
	* They only have to specify topic name and one broker to connect to, and kafka will automatically take care of routing the 
     data to the right brokers.

 Producers: Message keys
	* Producers can choose to send a key with the message
	* If a key is sent, then the producer has the guarantee that all the messages for that key go to the same partition.
	* This enables to guarantee ordering of the specific key.

Consumers
   	* Consumers read data from a topic
   	* They only have to specify the topic name and one broker to connect to, and kafka will automatically take care of 
       pulling the data from the right brokers.

Consumer Group
 	* Consumers read data in consumer groups
 	* Each consumer within a group reads from exclusive partitions
 	* You can't have more consumers than the partitions
 	* Kafka Broker manages the consumer groups, it acts as a group co-ordinator

 Consumer Offset
 	* Behave like a bookmark for the consumer to start reading the messages from the point it let off.