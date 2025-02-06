Kafka basic:
============
			1. Basic flow draw
			2. kafka client-1 (Producer)
						- synchoronous communication style(38)
						- asynchoronous communication style(39)
						- Producer configuration properties(41)
						- Acknowledgement-54
						- Retries-55
						- delivery and retries timeout
						- insyncreplica configuration and 
						- insyncreplica how it works
						- kafka producer spring Bean configuration
						- Producer Idempotent (application.properties and Spring Bean)


			3. Bootstrap server
			4. Kafka Broker
						- architecture
						- kRaft
						- cluster metadata
						- Interview and critical question from Broker

			6. Topic
						- replication factor
						- in-sync replica
						- partition and offset
						- Interview and critical question from Topic
						- when consumer failure happens, how to start reading from the latest stored offset? what is mean by commited offset?

			7. Partition
						- offset
						- reset-offset
						- shift-by
						- dry-run
						- by0duration
						- to-earlier
						- to-latest
						- to-datetime
						- execute

			8. kafka client-1 (Consumer)
								- messege ordering
								- multiple Consumer
								- Consumer group
								- @KafkaEventListener and @KafkaHandler explation
								- how rebalancing and partition assignment works
								- Multiple Consumers Consuming messages from Topic
								- Idempotent Consumer and and reading Unique_id with message Header 105/106
								- 



Kafka Advance:
==============
		1. Kafka Transaction
					- Isolation-level
					- Rollback transaction 119
					- reading commited message in kafka 120
					- Configure consumer MS to read 'commited" message only'
					- @Transaction annotation
					- local transaction with KafkaTemplate 123



		2. Kafka Error handling
				- Handle Deserialing error
				- Error handling deserializer
				- DLT How it works
				- handle Error DefaultErrorhandler and DeadLetterPublishingRecoverer
				- Exception handling in consumer and Retries
				- creating retryable and not retryable exception 90
				- DefaultErrorHandler with a list of not retryable exceptions 91
				- how not-retryable exception works 92
				- Throwing Retryble Exception 93



		3. Kafka Security
				- Kafka SSL


Evenet: something happen
Topic: way of organizing data within kafka cluster.
			- similer to table in a RDBMS
			- similar to a message queue
	- we can have thousands of topic!!
	- topic can have multiple partitions

kafka is open source Java API to implement MQs.

It is protocol independent, support load balancing for multiple Producer/Consumer using Multiple Message Broker.

It support data partitions for large data transfer.

It Support only Pub/Sub(default) no Queues.

Data is exchange in serialized format in Key=Value

Key = TopicName
Value = Data

Topic memory it contain data using TopicName (Multiple Topics)

R&D server is nothing but Zookeeper.
Cluster is collections of Message Broker(MB). when a consumer request to Zookeeper, then it will create a MB. data copied from Topic to MB. Zookeeper mainly manage/handle the lifecycle of MB.



Message Replica actually clone/read the data from Topic memory.

Topics are destination name, that store data in partition, given by producer and handled by Zookeeper

Data is stored in Topics with multiple segment/partition for big size data, id/index/offset is given for the pertition. If developer dont specify the partition size then the default partition size is 1. full data will stored as one.

Programmer has to give the partition size, topic name, replication factor etc.

Message Replication service : it is a subcomponent of zookeeper, It supports reading actal message and clone for consumer data transfer based on given topic name.

Consumer have to provide id, topicName, so that boodtrap (using zookeeper) connect with topic, take replica give to it meddage broker and transfer.

If Docker Error:
----------------------
Troubleshooting
If you have Docker Compose installed but still receive the error, make sure your environment variables are set correctly. Ensure /usr/local/bin is included in your PATH:

Add Docker Compose to PATH:


`export PATH=$PATH:/usr/local/bin`
Make the change permanent by adding the line to your shell's configuration file (e.g., ~/.bashrc, ~/.zshrc):

`echo 'export PATH=$PATH:/usr/local/bin' >> ~/.bashrc`


Apply the changes:
`source ~/.bashrc`
Once Docker Compose is installed and configured, you should be able to run docker-compose up -d without encountering the error.

kafka_container_id: 41d426191877
zookeeper_container_id: fb31f6e361a5

docker exec -it 41d426191877 kafka-topics --create --topic payment-topic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1

docker exec -it 41d426191877 kafka-console-producer --topic payment-topic --bootstrap-server localhost:9092
docker exec -it 41d426191877 kafka-console-consumer --topic payment-topic --bootstrap-server localhost:9092 --from-beginning


EDD with Kafka:
--------------

== Kafka Broker ==
 1. 3ta broker create korbo (3 bar server.properties copy paste kore)
 		- concern: node.id, listeners(these are network interfaces that kafka uses to communicate with other servers and clients.), log direcetory
 		configuration should be change.
 		- prepare storage directory/folder (unique cluster ID diye storage directory prepare korte hbe)
 			./bin/kafka-storage.sh format -t UUID -c config/kraft/server-1.properties
 			./bin/kafka-storage.sh format -t UUID -c config/kraft/server-2.properties
 			./bin/kafka-storage.sh format -t UUID -c config/kraft/server-3.properties

2. start kafka broker with Kraft
	./bin/kafka-server-start.sh config/kraft/server-1.properties

===> Reson of use key:value in producer
Ans: One of the reasons you would want to send a message with the key is because those messages that are sent with the same key , they are stored in the same partition and when messages are stored in the same partition, they are ordered. So, If you want to store and read messages in order, you will need to use the same key for those messages.

===> Partition Selection: 
To determine which partition to choose to store a message, Kafka will use a hash of a message key. If there is no key, then Kafka will equally distribute messages across multiple partitions using fmurmur/robin algorithm.


===>  if the --replication-factor is 5 and --config min.insync.replicas=2 then producer will wait for only acknowledgement from 2 replica. it will not slow down the kafka.

Broker Key points: 
------------------
1. Acknowledgement
2. In-Sync-Replica and Replication factor Relation
3. create a Kafka Cluster with 3 Broker
4. Retries: kotokkhon, kotobar, koi minute porpor
5. delivery timeout
6. Idempotent: 3 configuration must be remember
7. Producer ack error and mistakenly send same message duplicate.

Consumer:
=========
1. Consumer group for multiple same instance.
2. trusted.package configuration ta dekhte hbe
3. @KafkaEventListener and @KafkaHandler, @KafkaListener annotation
		= @KafkaListener(topics="TOPIC_NAME") - When you apply this annotation above,  it means that this method should be invoked whenever a new message is received from specified Kafka topic and the topic name you will provide in brackets here.
4. If you need to handle different type events in same config-class - tokhon annpkotation ta method er upore na dye class er upore dite hbe.
tokhon protita method @KafkaHandler diye annotate korte hbe.

So with this configuration, we are creating a Kafka listener class that will listen to events or messages, thats published to "product-created-events-topic".To specify which particular event your method is listening to, you will pass this event as a method argument like I'm doing it here, 
@KafkaHandler
public void handler(ProductCreateEvent productCreateEvent){
	
}

 and the handle method that I have created in this class. It will be invoked when Kafka consumer consumes message that is of a product created event data type.

==> What is the purpose of the @KafkaHandler annotation in a Kafka Consumer application?
Ans: 

==> What distinguishes the @KafkaHandler annotation from the @KafkaListener annotation in a Kafka Consumer application?
Ans: @KafkaHandler is used to handle specific message types within a @KafkaListener class, whereas @KafkaListener is used to define the method that listens to message from kafka topic

==> What is the difference between the spring.kafka.consumer.keydeserializer and spring.kafka.consumer.value-deserializer configuration properties in a Kafka Consumer application?

Ans:  keydeserializer- specifies the deserializer class for message keys
			value-deserializer- specifies the deserializer class for message values

==> In a Kafka Consumer application, what role does the spring.kafka.consumer.properties.spring.json.trusted.packages configuration play?
Ans: It determines the packages allowed for desirializing JSON messages, ensuring only object from known source are processed.

==> Can a single Kafka consumer consume messages from more than one topic?
Ans: Yes, A consumer can be confidured to consume message from multiple topics simutenoously.



72. creating core module:
76. this lecture is very important

Kafka consumer deserializer error(Error handling): using ErrorHandingDeserializeer.class


84: Dead letter Topic: 
85. This lecture is very important: Summery: 
 		-> create DefaultErrorHandler class instance inside consumer factory
 		-> register this error hander with KafkaListener.
 		-> create DeadLetterPublishingRecoverer(KafkaTemplate) class instance to DefaultErrorHandler() as parameter, the name of the dead letter topic will be just the same name as the name of the current topic from which.
 		-> DefaultErrorHandler errorHandler = new DefaultErrorHandler(new DeadLetterPublishingRecoverer(KafkaTemplate)); ----- And with this line of code here we say that use dead letter publishing recovery, to publish failed messages to the letter topic, when error occurs during message consumption by Kafka listener, and by default, the name of the dead letter topic will be just the same name as the name of the current topic from which this message was read, but it will have extension dot DLT.

 		KafkaTemplate - is what will actually be used to send that message to a dead letter topic. Because Kafka Template wraps Kafka Producer and provides methods to send messages to Kafka topic.

 		So since Kafka Template knows how to send messages to Kafka topic, it is the perfect tool for DeadLetterPublishingRecoverer to use when it needs to send failed messages to dead letter topic.

86: Create and cofigure KafkaTemplate object:
In this lesson, we will create and configure Kafka template object so that it can be used by the DeadLetterPublishingRecoverer class to actually send failed message to a dead letter topic, and to make KafkaTemplate be available in the spring application context, so that it can be injected by spring framework into this Kafka listener container factory method.

As method argument, I will need to create Kafka template object as a Bean.


@Bean
KafkaTemplate<String, Object> kafkaTemplate(ProducerFactory<String, Object> producerFactory){
	
	return new KafkaTemplate<>();
} 

So this method will create KafkaTemplate object. And because it is annotated with bin annotation, the Kafka template object that is returned from this method, it will be added to spring application context. And once we have Kafka template object in spring application context, we can inject it using spring dependency injection into other components and methods in our application.





Section-12: Exception and Retries:
===================================

eta ami bujhini, etar pichone onek time dite hbe.



Section-13: Consumer Group:
===========================

99. Rebalancing and Partition assiging in Kafka.
This Hands on lab is very Important for me.


 
Section-14: Idempotent Consumer in Kafka:
==========================================

max.pool.interval.ms=  this configuration property, it controls how much time Kafka Consumer has to process full messages. before it should pull a new batch of messages from Kafka topic.

If Kafka Consumer does not pull new messages from Kafka Broker longer than the time configured with this property, then Kafka Broker will assume that this consumer has failed, or it stopped and it will remove it from consumer group, and then it will trigger rebalance to reassign partitions to other consumers. so that in other instance of Kafka, consumer can consume and process this message.

If this happens, then this particular instance of consumer microservice, it will not be able to update partition offset.And this means that for Kafka Broker this message was not successfully consumed.


So what Kafka Broker will do is it will deliver the same message to another instance of the same microservice, or even to the same instance. But when this instance rejoins the group. But either way, the same message will be consumed again, and then Kafka Consumer will start processing the same message for the second time. It will again read from the database, start processing its main logic, and it will again write to the database, and at the end it will publish a new message to another topic. But this time it will be able to complete all the business logic in time and it will update partition offset.

 This will mean that this message is consumed successfully. But look what happened. We processed only one message, but there are two records in the database and we published two messages to another topic. And this is a big problem because if these are payment transactions, there was only one message with request to pay. But our Kafka consumer made two payments, so we need to prevent it.



105: Include a unique ID in message header: 
106: Reading Unique ID from message header.


Section-15: Apache Kafka Transaction:
=====================================

--> Idempotent Producer: helps to make sure that duplicate messages are not sent, 
--> Transactions: Ensure that consumer does not read message that is part of incomplete transaction.

Compensating Transactions: Be able to undo operations that spans multiple remote microservices.


126: This lecture is very important for me to understatnd


Section-15: SAGA design pattern with Apache Kafka:
==================================================

Choreography Based Saga: Microservice communicate with each other by exchanging events.
In Saga pattern, a MS will publish an event to perform compensating transaction.

==> In the Orchestration Saga pattern, who is responsible for coordinating the steps of a distributed transaction?
Ans: A Central Orchestrator (A central Controller)

==> In which Saga pattern is each local transaction publishing an event that triggers the next local transaction in the saga?
Ans: Choreography

==> Which Saga pattern would be more suitable for complex business transactions that require centralized control and decision making?
Ans: Orchestrator Saga

	

1. A distributed transaction is achieved through a series of asynchronous transactions across interconnected microservices.

2. Asynchronous behavior is the major advantage in Saga pattern which made it popular compared to well known 2 phase commit pattern.



Choreography based Saga:
------------------------

In a choreography-based saga, individual local transactions publish events that serve as triggers for other participants to carry out their respective local transactions.



Orchestration based Saga:
--------------------------

In an orchestrated-based saga, a centralized saga orchestrator communicates with saga participants by sending command messages, instructing them to execute their local transactions.





SAGA:
------

1. Saga Definition:
--------------------

A saga is a sequence of local transactions that together form a global transaction. Each local transaction can be performed by a different microservice, and each one can either succeed or fail. If one of them fails, the saga must roll back the previous transactions by executing compensating actions.

Saga is a way to manage a series of important actions and handle any problems along the way to keep everything in order and avoid chaos when things don't go as planned. It's used in computer systems to make sure complex tasks are completed correctly, step by step

Saga is long-running transactions across multiple microservices in a distributed system. It's a way of managing long-running operations where each microservice plays a part in a sequence of steps, ensuring that the entire process can either succeed as a whole or gracefully handle failures by undoing or compensating for completed steps


The Saga design pattern is a method used in distributed systems to maintain data consistency across multiple transactions or microservices. It's particularly useful in scenarios where traditional ACID transactions are not feasible due to the distributed nature of the system.

In a Saga pattern, a long-lived transaction is broken down into multiple smaller transactions, each of which is executed independently by the involved services. These smaller transactions are often referred to as "saga steps." If one of the steps fails, compensating transactions are executed to undo the changes made by the previously successful steps, ensuring that the system reaches a consistent state.

Choosing between choreography and orchestration for saga pattern implementation hinges on multiple factors. Choreography emphasizes decentralized communication among services, suited for scenarios with autonomous and loosely coupled services. It's beneficial when each service manages its transactions and compensating actions independently, enhancing scalability and resilience. Conversely, orchestration centralizes the coordination logic in a dedicated service, beneficial for complex workflows with dependencies or when a higher level of visibility and control is necessary.  #SagaPattern #Choreography #Orchestration #Microservices #TransactionManagement #DecentralizedCommunication #CentralizedControl.


2. What is choreography?
-------------------------

Choreography is a decentralized way of implementing sagas, where each microservice communicates with other microservices through events. There is no central coordinator that controls the flow of the saga. Instead, each microservice decides what to do based on the events it receives and publishes. The interactions between microservices are loosely coupled.

Choreography is a decentralized communication pattern in software systems. Components or services exchange events, each deciding when to perform their tasks. It's event-driven, loosely coupled, and allows for complex, asynchronous interactions.

Example-1: in a ride-sharing app, when a driver accepts a ride request, it emits an event that informs nearby drivers to stop searching for rides, and the user app to display the driver's location, all without a central controller. Each service to act based on local decisions and published events.


Example-2: Consider choreography as a team of dancers on a stage. Each participants responds to the music independently without a conductor. Here each dancer refers to individual microservice and they know when to perform the moves by listening to the rhythm of the events.

Pros and cons of choreography:
-----------------------------
		Advantage:
			- Reducing coupling between microservices, increasing scalability and availability.
			 Loose coupling(e.g. a payment service doesn't need to know about the order service's internal working).
			- Allowing for more flexibility and evolution. Flexibility(e.g. adding a new service can be integrated seamlessly without any adjustment to a central orchestrator).
			- Autonomy(e.g. an inventory microservice can independently without waiting for central instructions).
			- Easier maintenance(i.e. updating the logic in any of the service won't impact anywhere).	
			-  Scalability with decentralized operations(i.e. handling more amount of orders is easier as each order service can independently scale horizontally).
			- It's better for async flow but missing event need to handle properly for service continuity


		Disadvantage:
			- increased complexity and testing
			- reduced visibility and monitoring
			- Dependency on events.
			-  Complexity in understanding the flow.


3. What is orchestration?
-------------------------
Orchestration is a centralized way of implementing sagas, where a single microservice acts as a coordinator that commands other microservices to perform local transactions. The coordinator knows the logic and the order of the saga, and it communicates with other microservices through commands and replies.

Orchestration helps control, monitor, and automate processes, making them more efficient and reliable in computer systems.

In Orchestration model, there is a central component known as "Orchestrator" who is responsible for the execution of the individual steps which are known as saga activities in a predefined order. The orchestrator directly communicates with each microservices to initiate, monitor, handling the entire flow and compensate transactions based on the outcome each steps.

Example-1: Think of orchestration like a movie director guiding actors and actress through scenes. The director(orchestrator) has a script which is nothing but workflow that outlines how each actor/actress(microservice) should perform their respective tasks. The director coordinates when every scene start, how actor/actress interacts and when the movie reaches its conclusion.

Example: In the order saga, the coordinator might send a command to the inventory service to reserve a product, and wait for a reply. If the reply is positive, it might send a command to the payment service to charge the customer, and so on. If any of the commands fails, the coordinator might send compensating commands to the previous microservices to roll back the saga.

Pros and cons of orchestration:
------------------------------
Pros:
	- Orchestration has various advantages compared to choreography.
	- simplifying complexity and testing.
	- improving visibility and monitoring.
	- requiring less coordination and consistency.	
Cons:
	- it creates a single point of failure or bottleneck in the saga that can affect other microservices if one joins or leave
	- Increasing the coupling between microservices( Tight coupling).
	- decreasing scalability and availability.
	- limiting flexibility and evolution
	- Dependency on Orchestrator
	- Synchronous communication between services can impact scalability and responsiveness

With k8 and service registry/discovery, scalability is now not a problem in Orchestration approach as well. So only coupling is a major disadvantage in orchestration pattern.

	4. How to choose between choreography and orchestration:
	---------------------------------------------------------
Orchestration may be more efficient and consistent if communication is reliable and fast, whereas choreography may be more scalable and flexible if the saga is complex and frequent.


	Orchestration centralizes control and can simplify error handling, making it suitable for transactions requiring strong consistency. 

Choreography, promotes loose coupling and is more resilient to service failures, fitting for systems where eventual consistency is acceptable. 

The choice often hinges on the trade-off between control and flexibility. Hybrid approaches can leverage the strengths of both, tailoring the solution to the specific needs of the business process.


- Choreography is always better if there is no need of real time data consistency on the other hand orchestration is better if we need real time consistency of data.
-  if our priority is to gain control so the application will be more stable and more easily measurable and modifiable, we should consider the Orchestration .
- I understand that an orchestrated approach entirely based on event-driven architecture greatly facilitates the independence between services, enabling the addition of new services to a process without altering the existing ones. Another crucial aspect is its facilitation of visualizing distributed transactions and orchestrating processes to trigger retries and transaction compensation when needed.

Ref Link: - https://www.linkedin.com/advice/1/how-do-you-choose-between-choreography-orchestration
					- https://microservices.io/post/microservices/2019/07/09/developing-sagas-part-1.html