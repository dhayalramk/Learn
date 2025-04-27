- Link: https://www.tryexponent.com/blog/system-design-interview-guide
- Authors: [[Tom Lu]] , [[Neeraj Gupta]], [[Praveen Dubey]]
- Before starting this article, got doubt about [[HLD vs SLD]], so understood the basics
- Helpful tools to design: [[Tools / Whimsical]], [[Tools / Google Drawings]], [[Tools / Miro]]
- API Design Choices
	- Rest API
		- Properties: Resource Oriented, Data Driven, Flexible
		- Data: JSON, XML, YAML, HTML, Plain Text
		- Use Cases: Web based apps, cloud apps, client-server apps, cloud computing services, developer APIs
	- RPC
		- Properties: action-oriented, high performance
		- Data: JSON, XML, Thrift, Protobuf, FlatButters
		- Use Cases: complex microservice system, IoT Applications
	- GrapfQL
		- Properties: Single Endpoint, Strongly typed request, no data over fetching, self-documenting
		- Data: JSON
		- Use Cases: High performance mobile apps, complex systems and microservice based architectures
- Ways
	- Synchronous
		- Client -> (HTTP Sync) -> Service A's -> (HTTP Sync) -> Service B's
	- Async Messaging
		- Client -> (HTTP Sync) -> Service A's -> (Message) -> Queue -> (Message & Subscribe) -> Service B's
	- Publish - Subscribe
		- Client -> (HTTP Sync) -> Producer (Publish) -> Topic -> (Subscribe) -> Service A or Service B
- Scalability
  collapsed:: true
	- [[HLD / Replication]]
		- Is the data important enough to make the copies? How important is it to keep the copies the same?
			- Active Data -> (Data Replication) -> Mirrored Data
	- [[HLD / Partitioning]]
		- Partition contains a subset of the whole table. Each partition is stored on a separate server.
			- Horizontal Partitioning -> N1, N2,.., Nx -> Vertical Partitioning
	- [[HLD / Sharding]]
		- Sharding allows a system to scale as data increases, but not all data is suitable for sharding.
			- Collection 1 -> [Shard 1, Shard 2, Shard 3, ..., Shard N]
	- [[HLD / Load Balancing]]
		- Load Balancing distributes incoming traffic across multiple servers or resources.
			- Upload Service -> Load Balancer -> [Image Processor, Image Processor, Image Processer]
- Notes:
  collapsed:: true
	- G1
		- No. Items
		- Cache Miss & Hit
		- Disk & Memory Usage
	- G2
		- Write-Through
		- Read-Through
		- Write-Around
		- Write-Back
	- Popular caches:
		- In-memory
		- Redis
		- memcached
		- AWS Elasticcache
		- GCP Memorystore
	- Evictions:
		- LRU (Least Recently Used)
		- LFU (Least Freq. Used)
		- FIFO
		- MRU
		- Random Eviction
		- Least Used
		- On-Demand Expiration
		- Garbage Collections
	- G6
		- Storing user session
		- Communication between microservices
		- Caching frequent databases lookups
- Approach the problem
	- Step 1. Understanding the Problem - 10 Minutes
	  collapsed:: true
		- What are the fundamental and non-fundamental requirements?
		- What should be included and excluded?
		- Who are the clients and consumers?
		- Do you need to talk to pieces of an existing system?
		- Non functional requirements
			- Those may be related to business objectives or user experiences
			- includes
				- Availability
				- Consistency
				- Speed
				- Security
				- Reliability
				- Maintainablity
				- And Cost
			- To understand better from interviewer
				- What is the scale of the system?
				- How many users should it support?
				- How many requests should the server handle?
				- Are most use bases read-only?
				- Do users typically read the data shortly after someone else overwrites it?
				- Are most users on mobile devices?
			- Note:
				- If many design constrains, then focus on most critical one
					- Example: Social media design
						- Focus on photos and timeline generation services.
						- Lesser focus on: User registration and follow another user.
			- | Requirement     | Question                                                      |
			  |-----------------|---------------------------------------------------------------|
			  | Performance     | How fast is the system?                                       |
			  | Scalability     | How will the system respond to increased demand?              |
			  | Reliability     | What is the system’s uptime?                                  |
			  | Resilience      | How will the system recover if it fails?                      |
			  | Security        | How are the system and data protected?                        |
			  | Usability       | How do users interact with the system?                        |
			  | Maintainability | How will you troubleshoot the system?                         |
			  | Modifiability   | Can users customize features? Can developers change the code? |
			  | Localization    | Will the system handle currencies and languages?              |
		- Estimating Data
			- QPS (Queries Per Second)
			- Storage Size
			- Bandwidth requirement
	- Step 2: High-Level System Design - 10 Minutes
	  collapsed:: true
		- Types of API
			- Representational State Transfer [REST]
			- Simple Object Access Protocol [SOAP]
			- Remote Procedure Call [RPC]
			- or GrapgQL
		- Server and client communication
			- Ajax Polling
			- Long Polling
			- WebSockets
			- Server-Sent Events
			- |  | Pros | Cons |
			  | Ajax Pooling | Easy to Implement, works with all browsers | High Server load, high latency |
			  | Long Pooling | Low latency, less server load | High server load, not supported by all browsers |
			  | Websockets | Read-time communication | May require more complex server setup |
			  | Server - Sent Events | Efficient, Low latency | Unidirectional communication, not supported by all browsers |
		- Data Modelling
			- Creating a simplified schema that lists only the most important fields
			- Discussing data access patterns and the read-to-write ratio
			- Considering indexing options
			- And at a high level, identifying which database to use.
		- Database Cheat sheet for AWS, Azure, and Google Cloud
		- |  |  |  AWS | Azure | Google Cloud | Cloud Alternatives |
		  | Structured | ACID Transactions -> Relational | RDS, Aurora | Azure SQL Database | Cloud SQL, Cloud Spanner | MySQL, PostgreSQL, SQL Server, Oracle |
		  |  | Analytics (OLAP) -> Columnar | Redshift | Azure Synapse | BigQuery | Snowflake, ClickHouse, Druid, Pinot, Databricks |
		  | Semi-Structured | Nested Objects (XML, JSON) -> Document | Document DB | Cosmos DB | Firestore | MongoDB, Couchbase, Solr |
		  |  | Dictionary -> Key - Value | Dynamo DB | Cosmos DB | BigTable | Redis, ScyllaDB, Ignite | 
		  |  | Cache -> In-memory | ElastiCache | Azure Cache for Redis | Memory-store | Redis, Memcached, Ignite | 
		  |   | 2-D Key-Value  -> Wide column | Keyspaces | Cosmos DB | Bigtable | HBase, Cassandra, ScyllaDB | 
		  |  | Time Series -> Time Series | Timestream | Cosmos DB | BigTable, BigQuery | InfluxDB, ScyllaDB, Timescale | 
		  |  | Location & Geo-entities -> Geospatial | Keyspaces | Cosmos DB | BigTable, BigQuery | Solr, PostGIS, MongoDB | 
		  |  | Entity - Relationships -> Graph | Neptune | Cosmos DB | JanusGraph, BigTable | Neo4J, OrientDB, Giraph | 
		  | Unstructured | Full Text Search -> Text Search | OpenSearch, CloudSearch | Cognite Search | Cloud Search | Elasticsearch, Solr |
		  |  | (media) -> Blob | Amazon S3 | Blob Storage | Cloud Storage | HDFS, Cloudflare R2, MinIO |
		- Diagram for data and control flow explanation [[demonstrate - data & control flow]]
	- Step 3: Explore the Design: Deep-Dive - 10 Minutes
	  collapsed:: true
		- Non-Functional Requirements
			- Transactions: Database that offers ACID (Atomicity, Consistency, Isolation, and Durability) Properties
			- Data freshness: If an online requires fresh data, think about how to speed up the data ingestion, processing and query process
			- Data size: If the data size is small enough to fit into memory (up to hundreds of GBs), you can place it in memory. However, RAM is prone to data loss, so if you can't afford to lose data, you must find a way to make it persistent.
			- Partitioning: If the volume of data you need to store is large, you may want to partition the database to balance storage and query traffic
			- Offline processing: if some processing can be done offline or delayed, you may want to rely on message queues and consumers.
			- Access patterns: Revisit the data access pattern, QPS number, and read/write ration, and consider how they impact your choices for databases, database schemas, and indexing options.
	- Step 4: Improve the Design (Bottlenecks and Scale) - 10 Minutes
	  collapsed:: true
		- Are there any bottlenecks in this system? how well does it scale?
		- Evaluate if the system can operate effectively under different conditions and has the flexibility to support future growth.
		- Consider these points:
			- Single points of failure: Is there  a single point that could cause the entire system to fail? How could the system be more robust and maintain uptime?
			- Data replication: Is the data important enough to make copies? how important is it to keep all copies the same?
			- CDNs: Does it provide a service for people all over the world? Would data centers in different parts of the world make it faster?
			- High traffic: Are there any special situations, like when many people use the system simultaneously, that could make it slow or even break it?
			- Scalability: How can the system work for 10 times more people?
		- Message Queues and Public or Subscribe
			- By breaking down process and implementing queuing mechanisms to manage traffic, systems can be optimized for high performance at scale
			- Message Queues (MQs): MQs are ideal for scenarios where processing jobs in a specific order is essential. They ensure that tasks are executed sequentially, maintaining the integrity of the workflow.
			- Publish-Subscribe (Pub Sub) systems: PubSub systems shine when it comes to disseminating events or notifications to a large number of recipients concurrently.
		- Drawn the diagram of pub sub [[pubsub: example queues]]
			-
			-
		-
		-
	- Step 5: Wrap up
- Top Interview questions
	- Real Time Events
		- Design Face Messenger
		- Design Uber Eats
		- Design Whatsapp
		- Design Tinder
		- Design ChatGPT
	- Media & Content Delivery
		- Design YouTube
		- Design TikTok
		- Design Instagram
		- Design Netflix
		- Design Twitter
	- Async & Data Processing
		- Design a Web Crawler
		- Design a Metrics and Logging Services
		- Design Dropbox
		- Design a app to download user data
	- Payments & Marketplaces
		- Design a Parking Garage
		- Design Amazon Kindle Payments
		- Design a Hotel Booking Service
		- Design Zillow
		- Design a Vending Macine
		- Design Ticketmaster
	- Distributed Infrastructure
		- Design a key value store
		- Design a Rate Limiter
		- Design a Distributed Message Queue
		- Design a URl shortner
		- Design Typehead for Search
- Fundamental Principles and Concepts
	- Topics
		- Web Protocols
		- APIs
		- Reliablity
		- Availablity
		- Load Balancing
		- SQL vs NoSQL
		- Database Sharding
		- Database Replication
		- Consistent Hashing
		- Cap Theorem
		- Asynchronous Processing
		- Caching
		- Encryption
		- Authentication and Authorization
		- Cloud Architecture
		- CDNs
	- Web Protocols
		- Web protocols are the foundation of network communication, essential for the functioning of distributed systems. They include standards and rules for data exchange over a network, involving physical infrastructure like servers and client machines.
		- Network protocols ensure standardized communication amount machines, crucial for maintaining order and functionality in network interactions. The internet primarily uses two models, TCP/IP and OSI, to structure these communications.
		- TCP/IP Protocol and OSI Models
			- TCP/IP Protocol: Consists of four layers: Network Access, Internet, Transport and Application. It uses protocol like IP (Internet Protocol) and TCP (Transmission Control Protocol) to facilitate data transmission across network ideas.
			- OSI Model: A more conceptual, seven-layer model that provides a detailed breakdown of the network communication process.
		- TCP and UDP:
			- TCP: Focuses on reliable transmission, correcting errors like lost or out-of-order packets. It's suitable for applications where data accuracy is critical.
			- UDP: Offers faster transmission by eliminating error-checking processes. used in applications like live streaming where speed is preferred over accuracy.
		- HTTP and HTTPS
			- HTTP: An application layer protocol for transmitting hyperlinks and web content using request methods like GET and POST
			- HTTPS: Enhances HTTP with security features, encryption data to prevent unauthotized access.
		- TLS and Websockets
			- TLS (Transport Layer )
	-
	-