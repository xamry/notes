# OLAP
OLAP stands for Online Analytical Processing. It is a technology used in business intelligence systems to analyze and query multidimensional data. OLAP provides a way to organize and manipulate large volumes of data to support complex analysis and decision-making.

## OLAP Technology Types
### MOLAP
Multidimensional OLAP enables end-users to model data in a multidimensional environment, rather than providing a multidimensional view of relational data. It stored data in a cube (or also called **Hypercube**).

### ROLAP
Relational OLAP is a type of analytical processing that leverages the capabilities of a RDBMS to perform OLAP tasks.

### HOLAP
Hybrid OLAP is the product of the attempt to incorporate the best features of MOLAP and ROLAP into a single architecture.
HOLAP systems store larger quantities of detailed data in the relational tables while the aggregations are stored in the pre-calculated cubes.

### DOLAP
DOLAP systems often allow users to store and manage data locally on their desktop machines and it enables users to perform analytical tasks and interact with data locally on their own desktop or laptop machines.

### WOLAP
Web OLAP is OLAP system accessible via the web browser. 

### Mobile OLAP
Mobile OLAP helps users to access and analyze OLAP data using their mobile devices.

### SOLAP
Spatial OLAP is created to facilitate management of both spatial and non-spatial data in a Geographic Information system (GIS)

### HTAP
Hybrid Transactional/Analytical Processing refers to a database architecture that combines OLTP and OLAP capabilities within a single system. Different approaches such as in-memory databases, columnar databases, or distributed processing frameworks may be used to achieve HTAP capabilities.

## Schema Types
### Star Schema
Star schema is a data warehouse schema where there is only one “fact table" and many de-normalized dimension tables. Fact table contains primary keys from all the dimension tables and idwbitraining@gmail.com 6 other statistical columns (facts)

### Snowflake Schema
Unlike Star-Schema, Snowflake schema contain normalized dimension tables in a tree like structure with many nesting levels. Snowflake schema is easier to maintain but queries require more joins.

### Galaxy Schema

## Modelling Techniques
### ER Model 
In OLTP, for RDBMS. Focussed on normalization to reduce redundancy.

### Dimensional Modeling
In OLAP, for analytical processing. Focussed on making retrievals easy. 

Steps of dimensional modelling: 
1.  Identify Business Process
2.  Identify Grain (level of detail)
3.  Identify Dimensions
4.  Identify Facts
5.  Build Star

The model should describe the Why, How much, When/Where/Who and What of your business process

# Elements of Mutidimensional Data Model

## Dimension
A "dimension" is essentially an entry point for getting at the facts. Dimensions are things of interest to the business. In simple terms, they give **who**, **what**, **where** of a fact. Dimensions are nouns like date, store, inventory, etc.

### Dimension Table
-   A dimension table contains dimensions of a fact.
-   They are joined to fact table via a foreign key.
-   Dimension tables are de-normalized tables.
-   The Dimension Attributes are the various columns in a dimension table
-   Dimensions offers descriptive characteristics of the facts with the help of their attributes
-   No set limit set for given for number of dimensions
-   The dimension can also contain one or more hierarchical relationships
- 
### Types of Dimensions
#### Conformed Dimension
Conformed Dimensions (CD): these dimensions are something that is built once in your model and can be reused multiple times with different fact tables. Example: Time dimension

#### Junk Dimension
A "junk" dimension is a collection of random transactional codes, flags and/or text attributes that are unrelated to any particular dimension.

#### De-generated Dimension
A dimension which is located in fact table is known as Degenerated dimension. There are cases where a dimension attribute is not complex enough to warrant its own dimension table. Instead, it is directly included as an attribute in the fact table. This attribute becomes a degenerated dimension. Example: Transaction ID, Invoice ID etc.

#### Multi-Valued Dimension
A multi-valued dimension, also known as a multivalued attribute or repeating group, refers to a dimension attribute that can have multiple values associated with a single occurrence of an entity in a data model. Multiple values are stored directly within a single record of the dimension attribute.

#### Outrigger Dimension

#### Shrunken Dimension

#### Role-playing Dimension

#### Dimension to Dimension Table

#### Swappable Dimension

#### Step Dimension

#### Slowly Changing Dimension
Slowly changing dimensions refers to the change in dimensional attributes over time. 

An example of slowly changing dimension is a Resource dimension where attributes of a particular employee change over time like their designation changes or dept changes etc. There are three types of Slowly Changing Dimension:

 1. Type 1:  Update the existing row (no history)
 2. Type 2:  Add a new dimension row (history maintained)
 3. Type 3: Add additional column to maintain history (e.g. prior department)

## Fact
A "fact" is a numeric value that a business wishes to count or sum. 

### Fact Table 
A Fact Table in a dimensional model consists of one or more numeric facts of importance to a business. A Fact Table contains
1.  Measures
2.  Foreign key to dimension table

### Measures

### Types of Facts
There are three types of facts: 

#### Additive: 
Additive facts are facts that can be summed up through all of the dimensions in the fact table (Quantity Sold, Dollars Sold) 

#### Semi-Additive: 
Semi-additive facts are facts that can be summed up for some of the dimensions in the fact table, but not the others (Account Balance, Inventory levels) 

#### Non-Additive: 
Non-additive facts are facts that cannot be summed up for any of the dimensions present in the fact table (Room Temperature)

# OLAP Operations
## Roll-up
Roll-up is also known as “consolidation” or “aggregation.”

## Drill-down
In drill-down data is fragmented into smaller parts. It is the opposite of the rollup process.

## Slice 
Here, **one** dimension is selected, and a new sub-cube is created by filtering one or more values from that dimension. 
Slicing essentially "slices" the cube along the specified dimension, reducing the cube's size and focusing the analysis on a particular section of the data.

## Dice
Here you select **2 or more dimensions** and a new sub-cube is created by filtering one or more values from those dimensions.
Dicing provides a more detailed and focused view of the data by narrowing down the analysis based on multiple criteria.

## Pivot (rotate)
In Pivot, you rotate the data axes to provide a alternate presentation of data. It involves changing the orientation or structure of the cube to provide different perspectives on the data.

## Drill-through
Drill-through provides the ability to access detailed data underlying a summary value. It allows users to navigate from a summarized value to the transactional-level data for deeper analysis (usually in a different window).
Drill through provides a way to explore specific subsets of data in more depth without cluttering the main report or visualization with excessive details.
    
## Calculated Measures
Calculated measures are derived or computed measures based on existing measures and calculations. Calculated measures enable users to perform mathematical operations, apply formulas, and create custom calculations for analysis.
    
## Ranking
Ranking involves sorting data based on a particular measure to determine its relative position or rank within a dimension. It helps identify top performers, best-selling products, or other patterns in the data.
    
## Filtering
Filtering allows users to limit the data displayed in a cube or report based on specific conditions or criteria. It helps focus the analysis on subsets of data that meet certain requirements.
    
## Forecasting
Some OLAP systems offer forecasting capabilities to predict future trends and values based on historical data. Forecasting algorithms and models are used to generate predictions and support decision-making processes.



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg4MzMzMjI0MywxNzYxNDIwNjUzLDE1Nj
U1ODE0NjEsLTQ4MzIyMzYxMCwyMDE5NjU1ODE4LC0xNDM4MTg1
NjEwLC03OTQwMjkxMDIsMTQwMDYyMjg0OCwxMzExMzE2OTI4LD
EyNTk2ODQ5NTUsLTE5MTk3MTcyNTcsMTM3Nzc4MTU1NiwyNzc5
NzY1NjYsMTIyMzEwMTg0MCwtMTk0NjYwMDgwMywyMzc0OTIyMS
wtMTQ0MDYxNTM4NSwtMjE1NDMyNTQ0LDE0Njc2MTAxMjQsNTA1
NTM3MjQwXX0=
-->