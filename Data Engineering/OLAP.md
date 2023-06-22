# OLAP
OLAP stands for Online Analytical Processing. It is a technology used in business intelligence systems to analyze and query multidimensional data. OLAP provides a way to organize and manipulate large volumes of data to support complex analysis and decision-making.

## Schema Types
### Star Schema
Star schema is a data warehouse schema where there is only one “fact table" and many de-normalized dimension tables. Fact table contains primary keys from all the dimension tables and idwbitraining@gmail.com 6 other statistical columns (facts)
### Snowflake Schema
Unlike Star-Schema, Snowflake schema contain normalized dimension tables in a tree like structure with many nesting levels. Snowflake schema is easier to maintain but queries require more joins.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc1NTI3MzY5MiwtMjA4ODc0NjYxMl19
-->