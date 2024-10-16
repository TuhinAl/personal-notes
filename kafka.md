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
						- 
						- Interview and critical question from Topic

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
