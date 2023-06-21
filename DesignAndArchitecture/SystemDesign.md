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

# Scalability, Availability and Stability Patterns
https://www2.slideshare.net/jboner/scalability-availability-stability-patterns/18-How_do_I_know_if

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
 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIyNzUxODY1Nyw5NzQ1NjA1MSwxNTIwNT
cwMTQ1LC0xOTAxMTQzMTIzLDE5Mzg1MjMyMjYsLTk3OTkwNTMz
NCwxODEwNzMyMDY2LC0xNjU1MjY1NjgsLTE2MTcxNjM0ODAsLT
YzNTAzMjI5MywxMjkzNjAzMjUwLDEyNDI1NDYxODIsMTQzMjc0
NDcxMywtMTk2ODc4NTg4MywtMTQ3MzM4ODQ3OCwxNjQ4NDMyNT
U5LC0xMjc0NzY3MDAsLTkzMjAwNzUyLC05ODIwMjc3OTZdfQ==

-->