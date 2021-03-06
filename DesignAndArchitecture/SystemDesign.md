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
 - Performance Vs Scalability
 - Latency Vs Throughput
 - Availability Vs Consistency

## Availability Patterns
### Failover
### Replication
 - Master-slave
 - Tree replication
 - Master-master
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
eyJoaXN0b3J5IjpbOTc0NTYwNTEsMTUyMDU3MDE0NSwtMTkwMT
E0MzEyMywxOTM4NTIzMjI2LC05Nzk5MDUzMzQsMTgxMDczMjA2
NiwtMTY1NTI2NTY4LC0xNjE3MTYzNDgwLC02MzUwMzIyOTMsMT
I5MzYwMzI1MCwxMjQyNTQ2MTgyLDE0MzI3NDQ3MTMsLTE5Njg3
ODU4ODMsLTE0NzMzODg0NzgsMTY0ODQzMjU1OSwtMTI3NDc2Nz
AwLC05MzIwMDc1MiwtOTgyMDI3Nzk2XX0=
-->