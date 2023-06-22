# ETL
ETL stands for Extract, Transform, Load. It refers to a process used in data integration and management, particularly in the context of data warehousing and business intelligence.

## Difference between ETL and ELT
1. ETL loads data first into the staging server and then into the target system, whereas ELT loads data directly into the target system.
2. ETL is mainly used for on-premises, small amount of data and compute-intensive transformations (usually RDBMS), whereas ELT is used for large amounts of data, such as NoSQL, Hadoop cluster, scalable cloud installation, unstructured data etc.
3. ETL is easy to implement, whereas ELT requires niche skills to implement and maintain.
4. In case of ETL, Transformations are done in ETL server/staging area. In case of ELT, transformation is done directly in the target system (DWH).
5. ETL - Data first loaded into staging and later loaded into target system. Time intensive. ELT- Data loaded into target system only once. Faster.
6. ETL - Does not support data lake. ELT- Allows use of Data lake with unstructured data.
7. ETL - High costs for small and medium businesses. ELT - Low entry costs using online SaaS platforms.
8. ETL - The process is used for over two decades. It is well documented and best practices easily available. ELT - Relatively new concept and complex to implement.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjcyMTc1OTg1LC04MjMyMzMyNzAsLTE5OT
A3NDM0OTAsLTQ2NzcxMjY2NCwtMjk0ODM5NDY3LDczMDk5ODEx
Nl19
-->