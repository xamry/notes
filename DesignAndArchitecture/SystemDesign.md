## Use Cases
1. Pastebin/ URL shotener
2. Twitter TL + Search/
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
eyJoaXN0b3J5IjpbNzMwMDA1Mjk5LC0xOTY4Nzg1ODgzLC0xND
czMzg4NDc4LDE2NDg0MzI1NTksLTEyNzQ3NjcwMCwtOTMyMDA3
NTIsLTk4MjAyNzc5Nl19
-->