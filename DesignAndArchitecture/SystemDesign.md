## Use Cases
1. Pastebin/ URL shotener
2. Twitter TL + Search/FB TL + Search
3. Web Crawler
4. Mint.com
5. De
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

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEzMzc1Mjk4MiwtMTk2ODc4NTg4MywtMT
Q3MzM4ODQ3OCwxNjQ4NDMyNTU5LC0xMjc0NzY3MDAsLTkzMjAw
NzUyLC05ODIwMjc3OTZdfQ==
-->