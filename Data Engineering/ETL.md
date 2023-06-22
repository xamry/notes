# ETL
ETL stands for Extract, Transform, Load. It refers to a process used in data integration and management, particularly in the context of data warehousing and business intelligence.

## Difference between ETL and ELT
1. ETL loads data first into the staging server and then into the target system, whereas ELT loads data directly into the target system.
2. ETL is mainly used for a small amount of data and compute-intensive transformations (usually RDBMS), whereas ELT is used for large amounts of data, such as NoSQL, Hadoop cluster, cloud installation etc.
3. ETL is easy to implement, whereas ELT requires niche skills to implement and maintain.
4. In case of ETL, Transformations are done in ETL server/staging area. In case of ELT, transformation is done directly in the target system (DWH).
5. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA0ODkwNzEwMiwtODIzMjMzMjcwLC0xOT
kwNzQzNDkwLC00Njc3MTI2NjQsLTI5NDgzOTQ2Nyw3MzA5OTgx
MTZdfQ==
-->