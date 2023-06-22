# OLAP
OLAP stands for Online Analytical Processing. It is a technology used in business intelligence systems to analyze and query multidimensional data. OLAP provides a way to organize and manipulate large volumes of data to support complex analysis and decision-making.

## Schema Types
### Star Schema
Star schema is a data warehouse schema where there is only one “fact table" and many de-normalized dimension tables. Fact table contains primary keys from all the dimension tables and idwbitraining@gmail.com 6 other statistical columns (facts)
### Snowflake Schema
Unlike Star-Schema, Snowflake schema contain normalized dimension tables in a tree like structure with many nesting levels. Snowflake schema is easier to maintain but queries require more joins.

## Mutidimensional Data Model
### Fact
A "fact" is a numeric value that a business wishes to count or sum. 

### Dimension
A "dimension" is essentially an entry point for getting at the facts. Dimensions are things of interest to the business. Dimensions are a set of level properties that describe a specific aspect of a business, used for analyzing the factual measures.

### Fact Table 
A Fact Table in a dimensional model consists of one or more numeric facts of importance to a business. Examples of facts are as follows:  
the number of products sold 
the value of products sold
the number of products produced 
the number of service calls received
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI5ODg2NDA5OCwtMjA4ODc0NjYxMl19
-->