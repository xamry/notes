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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NzMzODg0NzgsMTY0ODQzMjU1OSwtMT
I3NDc2NzAwLC05MzIwMDc1MiwtOTgyMDI3Nzk2XX0=
-->