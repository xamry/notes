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
eyJoaXN0b3J5IjpbLTE5Njg3ODU4ODMsLTE0NzMzODg0NzgsMT
Y0ODQzMjU1OSwtMTI3NDc2NzAwLC05MzIwMDc1MiwtOTgyMDI3
Nzk2XX0=
-->