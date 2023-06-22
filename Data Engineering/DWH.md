# Data Warehouse
Data Warehouse is a "Subject-Oriented, Integrated, Time-Variant, Nonvolatile collection of data in support of decision making".

In general, a Data Warehouse is used on an enterprise level and a Data Marts is used on a business division/department level.

## DWH Properties

### Subject Oriented: 
Data that gives information about a particular subject instead of about a company's ongoing operations. 

### Integrated: 
Data that is gathered into the data warehouse from a variety of sources and merged into a coherent whole. 

### Time-variant: 
All data in the data warehouse is identified with a particular time period. 

### Non-volatile: 
Data is stable in a data warehouse. More data is added but data is never removed.

## Data Mart
Data mart is usually sponsored at the department level and developed with a specific details or subject in mind, a Data Mart is a subset of data warehouse with a focused objective.

 - Data mart are simpler to implement when compared to corporate Datawarehouse.
 - Compared to Data Warehouse, a datamart is agile.
 - Data Mart helps to enhance user’s response time due to reduction in volume of data
 - It provides easy access to frequently requested data.

### Types of Data Mart

 1. Dependent Data Marts: Dependent data marts are built directly from the data warehouse and rely on the data warehouse for their data. They are created by filtering and aggregating data from the data warehouse to meet the requirements of a particular department.
 2. Independent Data Marts: Independent data marts are standalone data marts that are created and maintained separately from the data warehouse. They may contain data from multiple sources, not just the data warehouse.

## ODS (Operational Data Sources)
Its a replica of OLTP system and so the need of this, is to reduce the burden on production system (OLTP) while fetching data for loading targets. Hence its a mandate Requirement for every Warehouse.

## Data Warehouse Architectures
### Centralized (EDW) Architecture
Single central EDW database

### Federated (Single department data mart) Architecture
Multiple data marts instead of an EDW, each for corresponding department.

### Multi-tiered Architecture
Combination of Single EDW + Multiple data marts.  Data is first written in EDF and then further copied to data marts.

## Three-Tier Data Warehouse Architecture
This is the most widely used Architecture of Data Warehouse.
1.  **Bottom Tier:**  The database of the Datawarehouse servers as the bottom tier. It is usually a relational database system. Data is cleansed, transformed, and loaded into this layer using back-end tools.
2.  **Middle Tier:** The middle tier in Data warehouse is an OLAP server which is implemented using either ROLAP or MOLAP model. For a user, this application tier presents an abstracted view of the database.
3.  **Top-Tier:** The top tier is a front-end client layer. Top tier is the tools and API that you connect and get data out from the data warehouse. It could be Query tools, reporting tools, managed query tools, Analysis tools and Data mining tools.

![Data Warehouse Architecture](https://www.guru99.com/images/1/022218_0735_DataWarehou2.png)

## Metadata
Metadata is data about data which defines the data warehouse. It is used for building, maintaining and managing the data warehouse.
Metadata helps to answer the following questions
-   What tables, attributes, and keys does the Data Warehouse contain?
-   Where did the data come from?
-   How many times do data get reloaded?
-   What transformations were applied with cleansing?

Metadata can be classified into following categories:

1.  **Technical Meta Data**: This kind of Metadata contains information about warehouse which is used by Data warehouse designers and administrators.
2.  **Business Meta Data:**  This kind of Metadata contains detail that gives end-users a way easy to understand information stored in the data warehouse.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY3Mjc4ODI5NSwxMDgyMDQ1ODQ3LC0xNj
I0NjQwMzU5LDg3NjI3MjAzNSw4MzA1NzI4LC0xMzE2MDUyNjA4
LC0xMjkzMjQ0MjQ4LDc3NDcyODEwMyw3MzA5OTgxMTZdfQ==
-->