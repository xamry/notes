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

## ODS (Operational Data Sources)
Its a replica of OLTP system and so the need of this, is to reduce the burden on production system (OLTP) while fetching data for loading targets. Hence its a mandate Requirement for every Warehouse.

## Three-Tier Data Warehouse Architecture
This is the most widely used Architecture of Data Warehouse.
1.  **Bottom Tier:**  The database of the Datawarehouse servers as the bottom tier. It is usually a relational database system. Data is cleansed, transformed, and loaded into this layer using back-end tools.
2.  **Middle Tier:** The middle tier in Data warehouse is an OLAP server which is implemented using either ROLAP or MOLAP model. For a user, this application tier presents an abstracted view of the database.
3.  **Top-Tier:** The top tier is a front-end client layer. Top tier is the tools and API that you connect and get data out from the data warehouse. It could be Query tools, reporting tools, managed query tools, Analysis tools and Data mining tools.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMTYwNTI2MDgsLTEyOTMyNDQyNDgsNz
c0NzI4MTAzLDczMDk5ODExNl19
-->