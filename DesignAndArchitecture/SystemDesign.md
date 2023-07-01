## Use Cases
1. Pastebin/ URL shotener
2. Twitter TL + Search/FB TL + Search
3. Web Crawler
4. Mint.com
5. Design a data structure for social network
6. Design a key-value store for search engine
7. Design Amazon's sales ranking by category feature
8. Design a system that scales to millions of users on AWS
9. 
## Distributed Transaction
(https://www.youtube.com/watch?v=S4FnmSeRpAY)  

Coordinator, Participants
### Two-Phase commit (Synchronous)
1. Prepare  
2. Commit  

### Three-Phase commit (Synchronous)
1. Can commit
2. Pre-commit
3. Do commit

### SAGA  (Async)
Separate microservice for failed transaction to rollback previous one.
Queues between microservice calls
Sequential events + Local transaction = Isolation

## Load Balancing
Load balancers distribute incoming client requests to computing resources such as application servers and databases.
Load balancers can be implemented with hardware (expensive) or with software such as HAProxy.
Additional benefits : SSL termination, Session persistence
To protect against failures, it's common to set up multiple load balancers, either in active-passive or active-active mode.
Load balancers can route traffic based on various metrics, including: Random, Least loaded, Session/cookies, Round robin or weighted round robin, Layer 4, Layer 7
Horizontal scaling via load balancers: Load balancers can also help with horizontal scaling, improving performance and availability.


# Scalability, Availability and Stability Patterns
https://www2.slideshare.net/jboner/scalability-availability-stability-patterns/18-How_do_I_know_if

## Scaling

### Vertical scaling 	
### Horizontal scaling
	* Load balancer, sticky session via external database or persistence cache
	* Cloning one instance via image (AMI) to ensure all nodes have the same codebase.
	* Database scaling. (NoSQL, Master-slave, Read replica, partitioning, federation)
	* Caching (im-memory- memcached/ redis) [Cached database queries, cached objects- recommended)
	* Asyncronism (Pre-building static pages beforehand, using a queue for a time consuming job and processing those jobs by an army of worker threads)


## Scalability Tradeoffs
###  Performance Vs Scalability
A service is said to be scalable if when we increase the resources in a system, it results in increased performance in a manner proportional to resources added. Increasing performance in general means serving more units of work, but it can also be to handle larger units of work, such as when datasets grow.
- If you have a performance problem, your system is slow for a single user.
- If you have a scalability problem, your system is fast for a single user but slow under heavy load.

### Latency Vs Throughput
 Latency is the time to perform some action or to produce some result.
Throughput is the number of such actions or results per unit of time.
Generally, you should aim for maximal throughput with acceptable latency.

### Availability Vs Consistency
Consistency - Every read receives the most recent write or an error (Weak/Strong/Eventual)
Availability - Every request receives a response, without guarantee that it contains the most recent version of the information
Partition Tolerance - The system continues to operate despite arbitrary partitioning due to network failures

CP - consistency and partition tolerance (Atomic read and writes)
AP - availability and partition tolerance   (Eventual consistency)

## Consistency Patterns
Weak consistency - After a write, reads may or may not see it. A best effort approach is taken.
Eventual consistency - After a write, reads will eventually see it (typically within milliseconds). Data is replicated asynchronously.
Strong consistency - After a write, reads will see it. Data is replicated synchronously.

## Availability Patterns
### Failover
Active-passive (Master-Slave): With active-passive fail-over, heartbeats are sent between the active and the passive server on standby. If the heartbeat is interrupted, the passive server takes over the active's IP address and resumes service.
Active-active (Master-Master): In active-active, both servers are managing traffic, spreading the load between them.

### Replication
 - Master-slave: The master serves reads and writes, replicating writes to one or more slaves, which serve only reads. 
 - Tree replication
 - Master-master : Both masters serve reads and writes and coordinate with each other on writes. If either master goes down, the system can continue to operate with both reads and writes.
 - Buddy replication

## Scalability Patterns
 - State
	 - Partitioning
	 - HTTP Caching
		 (Reverse proxy, CDN, Generate pre-computed static content) 
	 - RDBMS Sharding	
		 - Partitioning
		 - Replication
	 - NOSQL
		 BASE, Distributed Hash tables (DHT), Node ring with consistent hashing, 
	 - Distributed caching (EHCache, memcached, redis)
		 - Write-through
		 - Write-behind
		 - Eviction policies (TTL, FIFI, LIFO, Invalidate)
		 - Replication
		 - P2P
	 - Data Grids (Coherence, Terracotta, GemStone etc)
		 - Replication, partitioning, continuous availability, invalidation, fail-over, C+P)
	 - Concurrency
		 - Shared-state concurrency
		 - Message-passing concurrency
		 - Dataflow concurrency
		 - Software Transactional memory (STM)
 - Behavioral
 
## CDN

- Push CDN : Push CDNs receive new content whenever changes occur on your server. You take full responsibility for providing content, uploading directly to the CDN and rewriting URLs to point to the CDN. 
- Pull CDN: Pull CDNs grab new content from your server when the first user requests the content. You leave the content on your server and rewrite URLs to point to the CDN. 

## Reverse Proxy

A reverse proxy is a web server that centralizes internal services and provides unified interfaces to the public.
Additional benefits: Increased security, increased scalablity and flexibility, SSL termination, compression, caching, serve static content directly

## Caching

- Client caching
- CDN caching
- Web server caching
- Database caching
- Application caching

Data categories in cache:
⦁	Row level
⦁	Query-level
⦁	Fully-formed serializable objects
⦁	Fully-rendered HTML

When to update a cache: (Strategies)
⦁	Cache-aside
⦁	Write-through
⦁	Write-behind (or Write-back)
⦁	Refresh-ahead

## Asynchronism

Message queues (Redis, SQL, RabbitMQ)
Task Queues (Celery)

## Remote Procedure Call

Popular RPC frameworks: Protobuf, Thrift, and Avro.

## Representational state transfer (REST)

four qualities of a RESTful interface:
⦁	Identify resources (URI in HTTP) - use the same URI regardless of any operation.
⦁	Change with representations (Verbs in HTTP) - use verbs, headers, and body.
⦁	Self-descriptive error message (status response in HTTP) - Use status codes, don't reinvent the wheel.
⦁	HATEOAS (HTML interface for HTTP) - your web service should be fully accessible in a browser.





<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NjAyODEzOTYsLTUzNTU3MDc5Myw2Mz
IyMTI2OCwyMDgyMTU1MzM3LDk3NDU2MDUxLDE1MjA1NzAxNDUs
LTE5MDExNDMxMjMsMTkzODUyMzIyNiwtOTc5OTA1MzM0LDE4MT
A3MzIwNjYsLTE2NTUyNjU2OCwtMTYxNzE2MzQ4MCwtNjM1MDMy
MjkzLDEyOTM2MDMyNTAsMTI0MjU0NjE4MiwxNDMyNzQ0NzEzLC
0xOTY4Nzg1ODgzLC0xNDczMzg4NDc4LDE2NDg0MzI1NTksLTEy
NzQ3NjcwMF19
-->