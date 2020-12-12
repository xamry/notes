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
Sequential events + Local transaction = Isolation
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5MzI0MTcxNCwxNjQ4NDMyNTU5LC0xMj
c0NzY3MDAsLTkzMjAwNzUyLC05ODIwMjc3OTZdfQ==
-->