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
	 - Distributed caching
	 - Data Grids
	 - Concurrency
 - Behavioral
 

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkzODUyMzIyNiwtOTc5OTA1MzM0LDE4MT
A3MzIwNjYsLTE2NTUyNjU2OCwtMTYxNzE2MzQ4MCwtNjM1MDMy
MjkzLDEyOTM2MDMyNTAsMTI0MjU0NjE4MiwxNDMyNzQ0NzEzLC
0xOTY4Nzg1ODgzLC0xNDczMzg4NDc4LDE2NDg0MzI1NTksLTEy
NzQ3NjcwMCwtOTMyMDA3NTIsLTk4MjAyNzc5Nl19
-->