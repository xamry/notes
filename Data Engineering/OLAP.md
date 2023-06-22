# OLAP
OLAP stands for Online Analytical Processing. It is a technology used in business intelligence systems to analyze and query multidimensional data. OLAP provides a way to organize and manipulate large volumes of data to support complex analysis and decision-making.

## OLAP Technology Types
### MOLAP
Multidimensional OLAP enables end-users to model data in a multidimensional environment, rather than providing a multidimensional view of relational data. It stored data in a cube.

### ROLAP
Relational OLAP is a type of analytical processing that leverages the capabilities of a RDBMS to perform OLAP tasks.

### HOLAP
Hybrid OLAP is the product of the attempt to incorporate the best features of MOLAP and ROLAP into a single architecture.
HOLAP systems store larger quantities of detailed data in the relational tables while the aggregations are stored in the pre-calculated cubes.

### DOLAP
DOLAP systems often allow users to store and manage data locally on their desktop machines and it enables users to perform analytical tasks and interact with data locally on their own desktop or laptop machines.

### HTAP
Hybrid Transactional/Analytical Processing. It refers to a database architecture that combines real-time transaction processing (OLTP) and analytical processing (OLAP) capabilities within a single system.
# Schema Types
## Star Schema
Star schema is a data warehouse schema where there is only one “fact table" and many de-normalized dimension tables. Fact table contains primary keys from all the dimension tables and idwbitraining@gmail.com 6 other statistical columns (facts)

## Snowflake Schema
Unlike Star-Schema, Snowflake schema contain normalized dimension tables in a tree like structure with many nesting levels. Snowflake schema is easier to maintain but queries require more joins.

# Mutidimensional Data Model

## Dimension
A "dimension" is essentially an entry point for getting at the facts. Dimensions are things of interest to the business. Dimensions are a set of level properties that describe a specific aspect of a business, used for analyzing the factual measures.

### Slowly Changing Dimension
Slowly changing dimensions refers to the change in dimensional attributes over time. 

An example of slowly changing dimension is a Resource dimension where attributes of a particular employee change over time like their designation changes or dept changes etc.

#### Types of Slowly Changing Dimension

 1. Type 1:  Update the existing row (no history)
 2. Type 2:  Add a new dimension row (history maintained)
 3. Type 3: Add additional column to maintain history (e.g. prior department)

### Conformed Dimension
Conformed Dimensions (CD): these dimensions are something that is built once in your model and can be reused multiple times with different fact tables. Example: Time dimension

### Junk Dimension
A "junk" dimension is a collection of random transactional codes, flags and/or text attributes that are unrelated to any particular dimension.

### De-generated Dimension
A dimension which is located in fact table is known as Degenerated dimension. There are cases where a dimension attribute is not complex enough to warrant its own dimension table. Instead, it is directly included as an attribute in the fact table. This attribute becomes a degenerated dimension. Example: Transaction ID, Invoice ID etc.

### Multi-Valued Dimension
A multi-valued dimension, also known as a multivalued attribute or repeating group, refers to a dimension attribute that can have multiple values associated with a single occurrence of an entity in a data model. Multiple values are stored directly within a single record of the dimension attribute.

## Fact
A "fact" is a numeric value that a business wishes to count or sum. 

### Fact Table 
A Fact Table in a dimensional model consists of one or more numeric facts of importance to a business. Examples of facts are as follows:  
the number of products sold 
the value of products sold
the number of products produced 
the number of service calls received

### Types of Facts
There are three types of facts: 

#### Additive: 
Additive facts are facts that can be summed up through all of the dimensions in the fact table (Quantity Sold, Dollars Sold) 

#### Semi-Additive: 
Semi-additive facts are facts that can be summed up for some of the dimensions in the fact table, but not the others (Account Balance, Inventory levels) 

#### Non-Additive: 
Non-additive facts are facts that cannot be summed up for any of the dimensions present in the fact table (Room Temperature)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTczNTc4OTg0OCwtMjE1NDMyNTQ0LDE0Nj
c2MTAxMjQsNTA1NTM3MjQwLDM2ODI1OTgzLDE3OTE1NjI1MDYs
LTIwODg3NDY2MTJdfQ==
-->