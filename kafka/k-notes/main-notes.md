
`Note: I have collected this from internet, like random blog post, apache official docs, youtube and udemy. some diagram also created by me also.`

kafka is open source Java API to implement MQs.

1. kafka is open source Java API to implement MQs.
2. It is protocol independent, support load balancing for multiple Producer/Consumer using Multiple Message Broker.
3. It support data partitions for large data transfer.
4. It supports only Pub/Sub(default) no Queues.
5. Data is exchange in serialized format in Key=Value.
    Key = TopicName
     Value = Data

#### Events vs Messages:

Message is consist of Key, Value, Timestamp and Header. Here, Value is actually events. for example:
``` refer to the message_and_event link```

#### Bootstrap Server:
There are many servers in cluster. one/multiple (Multiple Brokers for Fault Tolerance) server initiate the connection between 
Kafka Client and Cluster.  The client uses these brokers to fetch metadata about the Kafka cluster, 
including information on all available brokers, topics, and partitions. Once connected to one or more bootstrap servers,
the client can then discover and connect to other brokers within the cluster as needed.

#### Zookeeper vs  KRaft ( handling metadata, coordination, and leader election within the Kafka brokers themselves)
R&D server is nothing but Zookeeper.
Cluster is collections of Message Broker(MB). when a consumer request to Zookeeper, then it will create a MB. 
data copied from Topic to MB. Zookeeper mainly manage/handle the lifecycle of MB.
<br>
<br>
`KRaft` is Kafka Raft which is a Raft protocol that follow raft consensus algorithm. 
It is basically used for select Leader and Follower in kafka broker. It simplifies architecture and enhances performance 
for modern Kafka clusters. <br>
`Zookeeper` is third-party server where KRaft is kafka-in-build. ZooKeeper support is currently phased out
from 3.8 version.
#### Topic and Partition:
`Topic memory:` it contains data using TopicName (Multiple Topics)

`Message Replica:` actually clone/read the data from Topic memory. <br>
`Topics:` are destination name,that store data in partition, given by producer and handled by Zookeeper.
Data is stored in Topics with multiple segment/partition
for big size data, id/index/offset is given for the partition. If developer don't specify the partition size then 
the default partition size is 1. full data will store as one. Programmer has to give the ```partition size, topic name, 
replication factor``` etc. 
Message Replication service : it is a subcomponent of zookeeper, It supports reading actual 
message and clone for consumer data transfer based on given topic name.Consumer have to provide id, topicName, 
so that bootstrap (using zookeeper) connect with topic, take replica give to it message broker and transfer.
<br>
<br>
**Broker Key points:**
1. Acknowledgement
2. In-Sync-Replica and Replication factor Relation
3. create a Kafka Cluster with 3 Broker
4. Retries: kotokkhon, kotobar, koi minute porpor
5. delivery timeout
6. Idempotent: 3 configuration must be remembered.
7. Producer ack error and mistakenly send same message duplicate.

<br>
<br>


#### Consumer:

1. Consumer group for multiple same instance.
2. trusted.package configuration ta dekhte hbe
3. @KafkaEventListener and @KafkaHandler, @KafkaListener annotation
   = @KafkaListener(topics="TOPIC_NAME") - When you apply this annotation above,  it means that this method should be invoked whenever a new message is received from specified Kafka topic and the topic name you will provide in brackets here.
4. If you need to handle different type events in same config-class - tokhon annpkotation ta method er upore na dye class er upore dite hbe.
   tokhon protita method @KafkaHandler diye annotate korte hbe.

So with this configuration, we are creating a Kafka listener class that will listen to events or messages, thats published to "product-created-events-topic".To specify which particular event your method is listening to, you will pass this event as a method argument like I'm doing it here,
```@KafkaHandler
public void handler(ProductCreateEvent productCreateEvent){

}
```
and the handle method that I have created in this class. It will be invoked when Kafka consumer consumes message that is of a product created event data type.



#### Broker:
#### 1. Definition and workflow
Broker is a Server, but it is not web server, It is actually kafka server.
Kafka Broker can be a physical computer, or it can be a virtual machine that runs Kafka processes.
And to make your system always available and faults tolerant, you can start multiple brokers in a cluster.
This way, if one of your Kafka brokers is down, you still have other brokers running and servicing requests from microservices. Behind the scenes.
<br>
<br>
These brokers work together to make sure that your events are stored reliably.
There will be one broker that will act as a leader, and all other brokers will act as followers.
Each of these brokers hosts Kafka topics, and each Kafka topic stores events in partitions.
<br>
<br>
The leader will handle all read and write requests for the partitions, while followers will passively
replicate leader's data. This way, **Kafka can achieve high availability and fault tolerance.**

Now, the leader and the follower roles are not fixed to a single broker, but can change dynamically
depending on the availability of the broker.

If a leader goes down for some reason, one of the follower brokers will become a new leader and will
continue servicing requests.

So, Kafka Broker is a software application that you will run on one or more computers.
Kafka broker will handle all the work to accept messages from producer, store it reliably in topic
partitions, and replicate it across other brokers in the cluster.
![alt text](/k-image/broker/broker-1.png)


#### 2. Leader Follower roles and Leadership balance:
Kafka Broker will act as a leader and other Kafka brokers will act as followers.

![alt text](/k-image/broker/broker-1.png)
In this diagram, I have three Kafka brokers. One Kafka broker acts as a leader, and other two Kafka brokers act as followers.

**A leader is responsible for handling all read and write requests for partitions in a topic.** 
It's called a leader because it leads or it manages all operations for topic partitions.

if your Kafka client wants to write a message into a topic partition, it will need to go through a leader. And once the 
message is successfully persisted in topic partition, it will be replicated to other Kafka brokers that act as followers.

Followers replicate data from the leader in exact order it was written, maintaining data consistency across cluster.

So leader is a single source of truth for all writes and reads in topic partition.
If followers were allowed to accept writes, it could lead to inconsistencies and conflicts because
**A follower in Kafka is a replica of a partition.**


If leader fails, one of the followers can take over.
But if you have only one broker in the cluster and if that broker goes down, then your entire system
is down and there is no replicas of your data.
So having multiple brokers in the cluster allows you to have more followers, and this helps you to
ensure high availability of the data.
If one broker including leader goes down, then data is still available through other brokers.


It is not always that the same Kafka broker is a leader, and all other Kafka brokers are always
followers.
If the same Kafka broker is always a leader, this will mean that all read and write operations are
always done through the same server, and this would create a bottleneck.
To avoid bottlenecks.
Every Kafka broker can be a leader and a follower at the same time.

Please See the Diagram:
![alt text](/k-image/broker/LF-1.png)
![alt text](/k-image/broker/LF-2.png)
![alt text](/k-image/broker/LF-3.png)

Kafka installing guide with `single-broker` and `multi-broker` with `KRaft` in Linux


The `controller.properties` file.It contains configuration for the server that acts as a controller, which is responsible for managing
the cluster metadata and coordinating the leader election for partitions.
<br>

The `broker.properties` file contains configuration for a server that acts as a broker, which is responsible for storing
and serving data for topics and partitions,
<br>
and `server.properties` file It contains configuration for a server that acts as both controller and broker.

Before I can start Kafka Server, there are a couple of commands that we need to run first.

**1. Generate unique ID for Kafka Cluster.**

go to `/kafka/bin/` and ran
```
./bin/kafka-storage.sh random-uuid

```

This will generate a unique identifier that you will need to use to configure your Kafka cluster.
```
example: GvWkgi3cQ-yB_g9ud5-XMw
```

** 2. Log directories **
The second command that I will need to run is to format log directories using this unique identifier.

```
./bin/kafka-storage.sh format -t <UUID> -c <PATH_TO_Configaration file(server.proerties)>
```
 with the `-c` parameter, I will need to specify the configuration file that I want to use for my Kafka server.
 So this will prepare the storage directories for running Kafka in Kraft mode.

** start Kafka server with configuration **
```
kafka/bin/kafka-server-start.sh kafka/config/kraft/server.properties
```
At this moment, this configuration file contains basic default configuration properties, 
which are enough for development purposes. Let's hit enter and my Kafka server is up and running.

#### Multiple kafka Broker

** How to start more than one Kafka server in a cluster. **

To start more than one Kafka server, I will need to create a new server property file for each new server.
go to `kafka/config/kraft/` and duplicate the `server.properties` file as how many broker you want to run.

let's assume that we want to start `three` Kafka servers. I will copy the server properties file and paste it three times.
rename these file to `server-1.properties`, `server-2.properties` and `server-3.properties`


NOTE: I still have my default `server.properties`, but I will not use it in this cluster. I will use it to start a single Kafka 
server with default configuration properties.

I will update just a few properties that I needed to start cluster of three servers.

```
server-1.properties:
--------------------


node.id=1
# This property is used to specify a list of listeners in Kafka Cluster.
# These are network interfaces that Kafka uses to communicate with other servers and clients.
# server.properties used to configure Kafka Server that performs two roles. A role of a broker and a role of a controller
# broker is listening on port number 9092, and the controller is listening on port number 9093
listeners=PLAINTEXT://:9092,CONTROLLER://:9093
# The next configuration property that I will update is Controller Quorum Voters.
#  this property is used to specify a list of quorum voters in Kafka cluster, which are the servers that act as controllers at this time.
# It is configured to use one server only, but we can specify more than one server here if needed.
# And this is what we will need to do if we want to run multiple servers in a single cluster the value of this property 
contains several pieces of information.
example node_id_of_the_controller@host_name_of_the_controller
controller.quorum.voters=1@localhost:9093,2@localhost:9095,3@localhost:9097

# The next configuration property that I will need to update is advertised.listeners.
# This is a name host and the port number the broker will advertise to its clients.
advertised.listeners=PLAINTEXT://localhost:9092

# the next configuration property that I will update will be the lock directory
log.dirs=/tmp/server-1/kraft-combined-logs
```

```
#server-2.properties
---------------------


 
node.id=2
listeners=PLAINTEXT://:9094,CONTROLLER://:9095
controller.quorum.voters=1@localhost:9093,2@localhost:9095,3@localhost:9097
advertised.listeners=PLAINTEXT://localhost:9094
log.dirs=/tmp/server-2/kraft-combined-logs
```



```
#server-3.properties
--------------------


node.id=3
listeners=PLAINTEXT://:9096,CONTROLLER://:9097
controller.quorum.voters=1@localhost:9093,2@localhost:9095,3@localhost:9097
advertised.listeners=PLAINTEXT://localhost:9096
log.dirs=/tmp/server-3/kraft-combined-logs
```

#### we will prepare a storage directory for Kafka cluster for three separate directory.

To prepare this storage directory for Kafka Server, we will need to first generate a unique identifier for our Kafka cluster.
Kafka stores its data like for example,` server logs, metadata and snapshots` . The path to this log directory we have configured in the server
dot properties file for each server(log.dirs=/tmp/server-3/kraft-combined-logs).

To prepare this storage directory for Kafka Server, we will need to first generate a unique identifier for our Kafka cluster.
go to `/kafka/bin/` and ran
```
./bin/kafka-storage.sh random-uuid

```

Then run

```
./bin/kafka-storage.sh format -t <UUID> -c <PATH_TO_Configaration file(server-1.proerties)>
./bin/kafka-storage.sh format -t GvWkgi3cQ-yB_g9ud5-XMw -c /kafka/config/kraft/server-1.properties
```
```
./bin/kafka-storage.sh format -t <UUID> -c <PATH_TO_Configaration file(server-2.proerties)>
./bin/kafka-storage.sh format -t GvWkgi3cQ-yB_g9ud5-XMw -c /kafka/config/kraft/server-2.properties
```
```
./bin/kafka-storage.sh format -t <UUID> -c <PATH_TO_Configaration file(server-3.proerties)>
./bin/kafka-storage.sh format -t GvWkgi3cQ-yB_g9ud5-XMw -c /kafka/config/kraft/server-3.properties
```

#### Start Multiple Kafka Broker

```
/kafka/bin/kafka-server-start.sh /kafka/config/kraft/server-1.properties
/kafka/bin/kafka-server-start.sh /kafka/config/kraft/server-2.properties
/kafka/bin/kafka-server-start.sh /kafka/config/kraft/server-3.properties
```

#### Stop Multiple Kafka Broker
**before shutting down your servers, it is a good practice to stop all running producers and consumers. This will also help
you avoid losing messages because if you stop your servers, they are down. But your Kafka producers keep on sending
messages to those offline servers. There is a chance that you lose those messages. Stopping producers and consumers first
also helps you to avoid errors in your system.**
`Ctrl + C  =` Kafka Server may not complete all graceful shutdown tasks like for example, closing log segments.
It will shut down, but not gracefully, and it might lead to problems.


A better way to stop one or multiple Kafka servers gracefully is to use CLI script `kafka-server-stop.sh`. This script is designed to 
shut down Kafka Server more gracefully.It allows Kafka Server to execute shutdown hooks and properly close down network 
connections, flush and commit any in-memory data to disk. Log segments are closed and any necessary cleanup is performed.
`controlled.shutdown.enable=true`

#### Kafka Topic

1. Create a new topic, 
2. List, 
3. Describe, 
4. Delete, 
5. Modify.

`bin/kafka-topics.sh --create --topic topic1 --partitions 3 --replication-factor 3 --bootstrap-server localhost:9092`

//todo need to add summary pdf

## Kafka Producer
#### producing Kafka Message without a Key:
`bin/kafka-console-producer.sh --bootstrap-server localhost:9092,localhost:9092 --topic TOPIC_NAME`
`auto.create.topics.enable=true` ---  Kafka is configured to automatically create a new topic if that topic does not exist.


#### producing Kafka Message with a Key:value:
`bin/kafka-console-producer.sh --bootstrap-server localhost:9092,localhost:9092 --topic TOPIC_NAME 
--property "parse.key=true" --property "key.separator=:"`
> key:value
> firstName:Alauddin
> 
> lastName:Tuhin
> 
> 
 //todo need to add summary pdf


Section-5:
-------------

 ### Consumer CLI: 
    1. Read new message only
    2. Read all messages from the beginning
`bin/kafka-console-consumer.sh --topic my-topic --from-beginning --bootstrap-server localhost:9092`
#### from beginning:
`bin/kafka-console-consumer.sh --topic my-topic --from-beginning --bootstrap-server localhost:9092`
#### read new message only:
`bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TOPIC_NAME `
#### Consuming Key:Value pair message:
`bin/kafka-console-consumer.sh --topic TOPIC_NAME --bootstrap-server localhost:9092  --property print.key=true
--property print.value=true --from-beginning`

#### Consuming Kafka message in order:

Kafka Topic is actually split into multiple partitions. To determine which partition to choose to store a message, 
Kafka will use a hash of a message key. If there is no key, then Kafka will equally distribute messages across multiple 
partitions using round-robin algorithm (or murmur algorithm). So even if you send those messages in order when you read 
them, their order might be different. **If you want to read messages in the order they were stored, these messages need to
use exactly the same key.** **If messages have the same key, they will be stored in the same partitions, they will
be read in the same order.**



#### Spring Boot Project as a Kafka Producer
Kafka producer is a spring boot microservice that publishes events to Kafka Broker. primary role of Kafka Producer is to 
publish messages or events to one or more Kafka topics. Before sending a message, Kafka producer serializes it into 
a byte array. Another responsibility of Kafka Producer is to _serialize messages to binary format_ that can be
transmitted over the network to Kafka brokers. Another responsibility of Kafka producer is to _specify the name of
Kafka topic_, where these messages should be sent.

When sending a new message to Kafka topic, we will also specify the partition where we want to store it, If neither 
partition nor key is provided, then Kafka producer will distribute messages across partitions in a round-robin fashion, 
ensuring a balanced load.
<br>
![alt text](/k-image/spring-project-producer/producer-task.png)
<br>
If a partition is not specified but a message key is provided, then Kafka will hash the key and use the result 
to determine the partition, and this ensures that all messages with the same key go to the same partition.Another
responsibility of Kafka producer is to choose which partition to write event data to.


#### Kafka Producer - Introduction to synchronous communication style


synchronous communication style is when sender sends a request and then waits for a response before proceeding.

In this project, we will use a special class from Spring Framework that is called Kafka Template. This class encapsulates 
Kafka Producer and provides a very user-friendly way to interact with Kafka from Spring Boot application. 

Example:

In above example, Order-microservice will create a new object. It will be called Order Created Event, and it will use 
Kafka-Producer to send a message to Kafka Broker. If orders microservice wants to know that the order created event was 
successfully stored in Kafka Broker, it will use Kafka Producer to send Kafka message using synchronous communication 
style, which means that it will wait for acknowledgement from Kafka Broker to confirm that the message was 
successfully received and stored before it proceeds with sending next message or performing other operations. Because Kafka Producer
is waiting to receive a response, it is blocked or it is on hold until the response from Kafka Broker is received.
<br>
![alt text](/k-image/spring-project-producer/synchronous.png)
<br>
In this diagram, I use synchronous communication style between mobile application and spring boot microservices
and between Kafka Producer and Kafka Broker.
#### Advantage/Benefit of synchronous communication
Using synchronous communication style between Kafka Producer and Kafka broker is considered to be more reliable because 
it ensures that message was successfully stored before moving on to the next task.

#### Disadvantage
But because producer is waiting, it can make your system just a little bit slower.

#### Asynchronous Communication
In those cases where high throughput and low latency is required, you might want to consider a different communication 
style that is called **asynchronous communication.**

#### Kafka Producer - A use case for asynchronous communication style

![alt text](/k-image/spring-project-producer/asynchronous.png)

#### Kafka Producer Configuration Properties


dependency
`	<dependency>
			<groupId>org.springframework.kafka</groupId>
			<artifactId>spring-kafka</artifactId>
   </dependency>`

**application.properties:**
```server.port=0

spring.kafka.producer.bootstrap-servers=localhost:9092,localhost:9094 // if you have more brokers in your cluster, 
                                                                then it is better to provide atleast two bootstrap servers
spring.kafka.producer.key-serializer=org.apache.kafka.common.serialization.StringSerializer
spring.kafka.producer.value-serializer=org.springframework.kafka.support.serializer.JsonSerializer

```

Kafka Configuration: Creating Kafka Topic: 

```@Configuration
public class KafkaConfig {
	@Bean
	NewTopic createTopic() {
		return TopicBuilder.name("product-created-events-topic")
				.partitions(3) //
				.replicas(3) //
				.configs(Map.of("min.insync.replicas","2")) 
				.build();
	}
}
```

**Partitions:** this allows for parallel processing and scalability. increasing number of partitions, increase the throughput.

**Replica:** Replica is a copy of topics data that is stored on a different broker. increasing number of replicas also increases 
the storage requirement and network traffic between brokers

**min.insync.replicas** : It specifies the minimum number of replicas that must acknowledge the write operation for this write operation to 
be considered as successful. So with this configuration, we say that when a message is sent to this topic, at least two 
replicas must acknowledge that the data is stored successfully.

![alt text](/k-image/broker/broker-2.png)

//Todo Spring Boot code snippet:
    event-class, service-class

#### Kafka Producer: Send Message Asynchronously:

published event to Topic:

```@Service
public class ProductServiceImpl implements ProductService {
	KafkaTemplate<String, ProductCreatedEvent> kafkaTemplate;
	@Override
	public String createProduct(CreateProductRestModel productRestModel) throws Exception {
		String productId = UUID.randomUUID().toString();
		ProductCreatedEvent productCreatedEvent = new ProductCreatedEvent(productId,
				productRestModel.getTitle(), productRestModel.getPrice(), 
				productRestModel.getQuantity());
		SendResult<String, ProductCreatedEvent> result = 
				kafkaTemplate.send("TOPIC_NAME",MESSAGE, VALUE_OR_EVENT).get(); // this is actually like CompletableFututre<SendResult<String, ProductCreatedEvent>> for synchronous nature without .get()
		return productId;
	}
}
```



### Kafka Producer: Retries and Acknowledgement
When Kafka producer sends a message, this message is sent to Kafka Broker. Kafka broker stores this message in Kafka topic. 
Inside the topic, Kafka message is stored in one of the partitions. Now, if your Kafka cluster has more than one broker
and proper replication factor configured, then topic partitions will be copied over to other brokers as well. In this case, 
one broker is a leader and it is the first one to receive Kafka message. It receives message and then it copies this 
message over to other brokers that act as followers, and these brokers that act as followers. They simply replica of the 
leader broker by default. Once leader broker stores message successfully, it sends acknowledgement to Kafka Producer 
that all is good, that it was able to successfully store the message and Kafka producer by default, it is configured 
to receive this acknowledgement from one broker only from leader, and this is a very good configuration. It is very 
useful configuration because it confirms that the received message is stored. But what if leader broker goes down 
before sharing this message with its followers and never comes back? In this case, the message is lost and to make 
our system more reliable, we can configure Kafka Producer to wait for acknowledgment from other brokers as well.

for Critical data lost scenario, producer to wait for acknowledgment from all in-sync replicas is good approach.
if the event/data critial is NOT important and it is okay if you lose some messages, you can configure your Kafka producer NOT to wait for any acknowledgment at all. To configure your Kafka producer to wait for acknowledgement from all brokers, you will use the following configuration property:

```
● spring.kafka.producer.acks=all  //Waits for an acknowledgement from all brokers.
● spring.kafka.producer.acks=1    //Waits for an acknowledgement from a leader broker only.
● spring.kafka.producer.acks=0    //Does not wait for an acknowledgement.
```

![alt text](/k-image/broker/replica-1.png)
To configure a Kafka producer to wait for acknowledgments, set acks to control durability:

1. `acks = "all"`: The producer waits for all in-sync replicas to acknowledge the record, providing strong durability guarantees since data won't be lost as long as one replica remains live.
2. `acks = "1"`: The producer waits only for the leader broker to acknowledge, offering lower latency but with the risk of data loss if the leader fails before followers replicate the data.
3. `acks = "0"` in Kafka lets the producer send messages without waiting for acknowledgments, enhancing speed but with no storage guarantees. This is ideal for non-critical data,
  such as frequent real-time updates (e.g., GPS coordinates) where occasional message loss is acceptable.

Using acks = "all" is more reliable, while acks = "1" balances durability with speed.

![alt text](/k-image/broker/replica-2.png)

Configuring Kafka producer acknowledgments to wait for all followers doesn’t mean it waits on every broker. 
Instead, it only waits for in-sync replicas (those up-to-date with the leader). The replication factor 
(set when creating a topic) determines how many brokers are in-sync, not the total broker count.

Additionally, by setting the minimum in-sync replicas (e.g., `min.insync.replicas=2`), you can specify
the minimum number of replicas needed for an acknowledgment. This allows the producer to respond faster, 
as it doesn’t wait for all replicas, only the configured minimum—ensuring reliability with faster performance.

#### Producer Retries:
Kafka producer configurations help manage message delivery and retries effectively:

1. **Minimum In-Sync Replicas:** Setting this to "3" means the producer waits for acknowledgments from the leader 
  and two other in-sync replicas, ensuring data reliability.
2. **Retry Behavior:** When a replica is unavailable, Kafka retries until reaching the delivery timeout (default: 2 minutes).
   Errors can be temporary (e.g., network issues) or permanent (e.g., oversized messages). Retries and retry backoff (default: 100ms) 
   help manage temporary errors by spacing retry attempts.
3. **Delivery Timeout:** Controls max time for message delivery and retries (default: 2 minutes).
4. **Linger:** Defines the wait time before sending message batches, improving performance for large messages and throughput
   when set higher.
5. **Request Timeout:** Sets the max wait time for a broker acknowledgment per request, distinct from delivery timeout 
   which covers the entire send process, retries, and acknowledgment.

These settings help balance performance, reliability, and latency in Kafka messaging.
![alt text](/k-image/producer/producer-retries-1.png)<br>

I have set the minimum in sync replicas property (`--config min.insync.replicas=3`) with a value of three.This means that
my Kafka producer will wait for acknowledgement from the Leader, and it will wait for acknowledgement from other
two additional in-sync replicas.

But what happens if one of the followers goes down and we don't have this in sync replica
at the moment? The default behavior of Kafka producer in this case is to retry the send operation for a very large number
of times, or until the delivery timeout is reached, and the default timeout value is two-minutes.

![alt text](/k-image/producer/producer-retries-2.png)<br>


`spring.kafka.producer.retries=10` property: it determines how many times producer will try to send the message before marking it as failed.
Producer will try up to ten times before giving up and raising an exception.

`spring.kafka.producer.properties.retry.backoff.ms=1000` you can figure how long Kafka Producer will wait before we try 
the failed request. It helps to avoid repeatedly sending requests. Kafka producer will wait for one second before retry.
In Kafka documentation it is mentioned that developers are encouraged to control the retry behavior with a different configuration property.

`spring.kafka.producer.properties.delivery.timeout.ms=120000` use this configuration property to configure the maximum time.
Producer should wait for a message to be delivered before raising a timeout exception.
 
![alt text](/k-image/producer/producer-retries-3.png)<br>

![alt text](/k-image/producer/producer-retries-4.png)<br>


#### Configure Producer Acknowledgments in Spring Boot Microservice: 
**application.properties:**

```
spring.kafka.producer.acks=all
#spring.kafka.producer.retries=10
#spring.kafka.producer.properties.retry.backoff.ms=1000

spring.kafka.producer.properties.delivery.timeout.ms=120000
spring.kafka.producer.properties.linger.ms=0
spring.kafka.producer.properties.request.timeout.ms=30000
```

#### Lesson:60 - How Kafka Producer Retries works:
    //Todo [57-62 lecture ratre dekhb]

#### Kafka Producer Spring Bean configuration:

```
@Configuration
public class KafkaConfig {
	@Value("${spring.kafka.producer.bootstrap-servers}")
	private String bootstrapServers;

    @Value("${spring.kafka.producer.key-serializer}")
    private String keySerializer;

    @Value("${spring.kafka.producer.value-serializer}")
    private String valueSerializer;

    @Value("${spring.kafka.producer.acks}")
    private String acks;

    @Value("${spring.kafka.producer.properties.delivery.timeout.ms}")
    private String deliveryTimeout;

    @Value("${spring.kafka.producer.properties.linger.ms}")
    private String linger;

    @Value("${spring.kafka.producer.properties.request.timeout.ms}")
    private String requestTimeout;
	
	Map<String, Object> producerConfigs() {
		Map<String, Object> config = new HashMap<>();
		
		config.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrapServers);
		config.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, keySerializer);
		config.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, valueSerializer);
		config.put(ProducerConfig.ACKS_CONFIG, acks);
		config.put(ProducerConfig.DELIVERY_TIMEOUT_MS_CONFIG, deliveryTimeout);
		config.put(ProducerConfig.LINGER_MS_CONFIG, linger);
		config.put(ProducerConfig.REQUEST_TIMEOUT_MS_CONFIG, requestTimeout);
		
		return config;
	}
	
	@Bean
	ProducerFactory<String, ProductCreatedEvent> producerFactory() {
		return new DefaultKafkaProducerFactory<>(producerConfigs());
	}
	
	@Bean
	KafkaTemplate<String, ProductCreatedEvent> kafkaTemplate() {
		return new KafkaTemplate<String, ProductCreatedEvent>(producerFactory());
	}
	
	@Bean
	NewTopic createTopic() {
		return TopicBuilder.name("product-created-events-topic")
				.partitions(3)
				.replicas(3)
				.configs(Map.of("min.insync.replicas","2"))
				.build();
	}
}
```

#### Producer Idempotent
update KafkaConfig class
       
```      
        @Value("${spring.kafka.producer.properties.enable.idempotence}")
        private boolean idempotence;
        
        @Value("${spring.kafka.producer.properties.max.in.flight.requests.per.connection}")
        private Integer inflightRequests;
        
        config.put(ProducerConfig.ENABLE_IDEMPOTENCE_CONFIG, idempotence);
        config.put(ProducerConfig.MAX_IN_FLIGHT_REQUESTS_PER_CONNECTION, inflightRequests);
   
   ```

**Idempotent Explanation:**

`An Idempotent producer avoids duplicate messages in the log in the presence of failures and retries.`

Kafka producer and on the right side of my diagram I have Kafka Broker. Kafka producer will send a message to Kafka Broker.
Broker will receive this message and it will store it in Kafka topic. Once the message is successfully stored, Kafka Broker 
will send back acknowledgement. This is a happy path scenario, but because Kafka producer and Kafka broker they communicate
with each other over the network, it is possible that a network error can take place and this acknowledgement will not 
reach Kafka. Producer. If producer retries are configured, then producer will send the same message again. Broker will 
receive this message and it will store it in Kafka topic again. Once the message is stored, Kafka Broker will send
acknowledgement to Kafka Producer and this time acknowledgement will pass through and Kafka Producer will receive it
successfully. Now the problem here is that we now have two identical messages in Kafka topic.

In simple words, this means that producer can send the same message multiple times, but Kafka Broker will only store it 
once and keep it in the correct order, and this can prevent inconsistency in Kafka topic, even if there are problems 
with the network or servers.


Once you enable Idempotence in your Kafka producer, your application will work this way.Producer will send a message.
Kafka broker will store this message in Kafka topic and once the message is stored, Kafka Broker will send acknowledgement
back to producer.If network problem takes place and this acknowledgement does not reach Kafka producer, then our producer
will send the message again.

because we have enabled Idempotence in our producer, Kafka broker will see that producer is sending the same message again.
And there is already a message like this in Kafka topic.Instead of storing the same message again, Kafka Broker will simply
acknowledge that it does have already this message.And in this case, if Kafka producer sends the same message multiple times, 
there will be only one such message in the topic and there will be no duplicates.

To enable idempotent in your Kafka producer, you will need to set the following configuration property:
`enable.idempotence=true`
**application.properties:**
`spring.kafka.producer.properties.enable.idempotence=true`

**@Bean:**
`props.put(ProducerConfig.ENABLED_IDEMPOTENCE_CONFIG, true);`

However, it is still recommended to explicitly set this property to true because it is very easy to disable it,
If this property is not explicitly set to true, then you can accidentally disable Idempotence by setting the following 
configuration properties to conflicting values:

```
acks=all
retries=2142445322
max.in.flight.request.per.connection=5
```

this configuration means that Kafka producer can send up to five requests or batches of messages to broker at the same 
time without waiting for acknowledgements.

```
spring.kafka.producer.properties.acks=all
spring.kafka.producer.properties.retries=214783647
spring.kafka.producer.properties.max.inflight.requests.per.connection=5
spring.kafka.producer.properties.enable.idempotence=true
```

it also introduces risk of message reordering in case of failures and retries, and keeping it at five is important for 
idempotent producer to maintain the right order and to avoid message loss.



## Kafka Consumer:

In this section we will create email-service as Kafka consumer, it will be consuming new messages from Kafka topic. 
when Kafka consumes message from a topic, it does not delete it. From there, the message remains in the topic. So if needed,
you can have more Kafka consumers running, and each of these Kafka consumers will receive their own copy of a message.


when you start consumer microservice, it starts pulling messages from Kafka topic at a regular time interval, which 
can be configured through configuration properties. Kafka consumer reads messages from partitions, it reads them in parallel.
There is no order guarantee which messages from which partitions will be read first, but it does read messages in order 
within a single partition.

![alt text](/k-image/consumer/consumer-1.png)

Messages within a single partition they are always read in order, but there is no order guarantee between partitions.
For example, there is no guarantee that messages from partition one will always be read before messages from partition two.
If you have a single application, then it will read messages from all three partitions. if you have three consumers 
running, then each consumer will be assigned to read messages from one partition only.


If you need to scale up your application and you want to start more instances of the same consumer microservice,
then this instances of Kafka consumer, they can be grouped together and work as a group.This way, instead of one consumer, 
you will have three consumers reading messages from the same topic,each consumer reading messages from its own partition.
And this will help you process messages from Kafka topic faster.


**`Kafka consumer reads message from Kafka topic, it does not delete this message from the topic.`**
The message remains in the topic until it is deleted from there automatically. By default, Kafka Topic is configured 
to keep messages for 168 hours, which is seven days, but if needed, you can change this value using Configuration
properties file.


server.port=0
spring.kafka.consumer.bootstrap-servers=localhost:9092,localhost:9094
#spring.kafka.consumer.key-deserializer=org.apache.kafka.common.serialization.StringDeserializer
#spring.kafka.consumer.value-deserializer=org.springframework.kafka.support.serializer.JsonDeserializer
spring.kafka.consumer.group-id=product-created-events
spring.kafka.consumer.properties.spring.json.trusted.packages=com.appsdeveloperblog.ws.core