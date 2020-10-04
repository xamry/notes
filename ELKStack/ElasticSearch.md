# Setup Elastic Search


### Install Elasticsearch

    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -  
    sudo apt-get install apt-transport-https  
    echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list  
    sudo apt-get update  
    sudo apt-get install elasticsearch  

### Configure it

    sudo vi /etc/elasticsearch/elasticsearch.yml  
    
    node.name: node-1  
    network.host: 0.0.0.0  
    discovery.seed_hosts: ["127.0.0.1"]  
    cluster.initial_master_nodes: ["node-1"]  

### Start elasticsearch and configure to start it automatically with ubuntu

    sudo /bin/systemctl daemon-reload  
    sudo /bin/systemctl enable elasticsearch.service  
    sudo /bin/systemctl start elasticsearch.service  

### Test connection

    curl -XGET 127.0.0.1:9200  

# Play around with some data

### Download schema

    wget http://media.sundog-soft.com/es7/shakes-mapping.json  

### Put the schema inside ES (i.e. create Index)

    curl -H "Content-Type: application/json" -XPUT 127.0.0.1:9200/shakespeare --data-binary @shakes-mapping.json  

### Download some data

    wget http://media.sundog-soft.com/es7/shakespeare_7.0.json  

### Put the data inside index

    curl -H "Content-Type: application/json" -XPOST '127.0.0.1:9200/_bulk' --data-binary @shakespeare_7.0.json  

### Search a string

    curl -H "Content-Type: application/json" -XGET '127.0.0.1:9200/shakespeare/_search?pretty' -d '  
    {  
      "query" : {  
        "match_phrase" : {  
        "text_entry" : "to be or not to be"  
        }  
      }  
    }'  

# Mapping and Indexing data

## Connecting to your cluster

### Open SSH, ES and Kibana ports on your VM
VM -> Settings -> Network -> Advanced -> Port Forwarding -> Add (+)  

    Name = SSH  
    Protocol = TCP  
    Host IP = 127.0.0.1  
    Host Port = 22  
    Guest Port = 22  
    
    Name = Elasticsearch  
    Protocol = TCP  
    Host IP = 127.0.0.1  
    Host Port = 9200  
    Guest Port = 9200  
    
    Name = Kibana  
    Protocol = TCP  
    Host IP = 127.0.0.1  
    Host Port = 5601  
    Guest Port = 5601  

#### Connect to Ubuntu machine using PuTTY/ Terminal using SSH
In real world, you would usually never login to Elasticsearch machine directly. You would SSH to it from a remote machine.  


## Download dataset

Download movielens dataset from http://files.grouplens.org/datasets/movielens/ml-latest-small.zip  


## Mappings
### Common Mappings
#### Field Types

    "type" : "String|byte|short|integer|long|float|double|boolean|date"

#### Field Index
Whether analyzed or not (whether exact match or partial match)
 
    "index" : "not_analyzed"

#### Field Analyzer
Define your character filters, tokenizer and token filter  
Character Filter - For example remove HTML encoding, convert & to and etc.  
Tokenizer - Split strings on whitespaces, punctuations, non-letters etc.  
Token Filter - Lowercasing, stemming, synonyms, stopwords etc.  

    "analyzer" : "standard|whitespace|simple|english"  

## Indexing a single document
### Write your own curl
To avoid typing -h "Content-Type: application/json" every time  

    mkdir bin
    cd bin  
    vi curl  
    #!/bin/bash  
    /usr/bin/curl -H "Content-Type:application/json" "$@" 
    chmod a+x curl    
    cd ~   
    source .profile  
    which curl  

### Create Mapping

    curl -XPUT localhost:9200/movies -d '  
    {  
        "mappings" : {  
            "properties" : {  
                "year" : {  
                    "type" : "date"  
                }           
            }       
        }  
    }'  

    curl -XGET localhost:9200/movies/_mapping  

### Insert a document

    curl -XPOST localhost:9200/movies/_doc/109487 -d '  
    {  
        "genre" : ["IMAX", "Sci-Fi"],  
        "title" : "Interstellar",  
        "year" : 2014  
    }'  

    curl -XGET localhost:9200/movies/_search?pretty

## Use Bulk API to index multiple documents
### Download the dataset to bulk index
The Bulk API accepts dataset in JSON format, so let's download it

    wget http://media.sundog-soft.com/es7/movies.json

### Bulk index documents from the file 

    curl -XPUT localhost:9200/_bulk?pretty --data-binary @movies.json

(or you could have used -d 'Entire JSON' option as well)

### Print the indexed documents

    curl -XGET localhost:9200/movies/_search?pretty

## Updating a document
Elasticsearch documents are immutable
But every document has a _version field.
When we update a document, an new document with incremented _version is created, while the older document is marked for deletion.
Elasticsearch will do a cleanup operation at an appropriate time at later stage.

### Updating existing document using PUT
You have to provide the entire data as if you're inserting entire new document
     curl -XPUT localhost:9200/movies/_doc/109487?pretty -d '
     {
    	 "genre" : ["IMAX", "Sci-Fi"],
    	 "title" : "Interstellar 2",
    	 "year" : 2014
     }'
Notice the _version (it will change to 2)

    curl -XGET localhost:9200/movies/_doc/109487?pretty

### Updating existing document using POST
You can provide only the field you want to change
curl -XPOST localhost:9200/movies/_doc/109487/_update -d '

    {
    	"doc" : {
    		"title" : "Interstellar"
    	}
    }'

    curl -XGET localhost:9200/movies/_doc/109487?pretty

## Deleting documents
Delete the movie Dark Knight

### First search the document

    curl -XGET localhost:9200/movies/_search?q=Dark

### Delete the document

    curl -XDELETE localhost:9200/movies/_doc/58559?pretty

## Dealing with concurrency
### Optimistic Concurrency Control
_seq_no  : Sequence number of document
_primary_term : Primary shard that owns that sequence

Change a records specifying _seq_no and _primary_term
Only one of the client will succeed if using the same sequence number and primary term
If sequence number was already incremented for other client, elasticsearch will throw an error for this client
Manually retry update with fresh sequence number and primary term, OR use retry_on_conflict=N to automatically retry

### Update a document for given sequence

     curl -XPOST "localhost:9200/movies/_doc/109487?if_seq_no=6&if_primary_term=2" -d '
    {
    "title" : "Interstellar 2"
    }'
Try updating with the same sequence number and primary term, and ES would throw version_conflict_engine_exception.

    [109487]: version conflict, required seqNo [6], primary term [2]. current document has seqNo [12] and primary term [3]"

Update using retry_on_conflict:

    curl -XPOST "localhost:9200/movies/_doc/109487/_update?retry_on_conflict=5" -d '
    {
    "doc": {
    	"title" : "Interstellar 4"
    	}
    }'
    
## Using Analyzers and Tokenizers
### Default Behavior
Example of partial match: Searching All movies with Star Trek in title (Notice the score in search result)   

     curl -XGET localhost:9200/movies/_search?pretty -d '
        {
        	"query" : {
        		"match": {
        		"title" : "Star Trek"	
        	}
           }
        }'
Example of lowercasing and partial match:

    curl -XGET localhost:9200/movies/_search?pretty -d '
            {
            	"query" : {
            		"match_phrase": {
            		"genre" : "sci"	
            	}
               }
            }'
### Change the default behavior
#### Recreate the Index with modified mappings
Make genre keyword match, and apply english analyzer on title

    curl -XDELETE localhost:9200/movies
    curl -XPUT localhost:9200/movies -d '
    {
    	"mappings": {
    		"properties": {
    		"id": {"type" : "integer"},
    		"year" : {"type" : "date"},
    		"genre" : {"type" : "keyword"},
    		"title" : {"type" : "text", "analyzer" : "english"}	
    	}
       }
    }'
    curl -XPUT localhost:9200/_bulk?pretty --data-binary @movies.json

### Check search behavior again after modified mappings
Returns nothing (Has to be exact match Sci-Fi, case sensitive)

     curl -XGET localhost:9200/movies/_search?pretty -d '
                {
                	"query" : {
                		"match_phrase": {
                		"genre" : "sci"	
                	}
                   }
                }'
Returns both Star Trek and star wars, due to analyzer:

    curl -XGET localhost:9200/movies/_search?pretty -d '
            {
            	"query" : {
            		"match": {
            		"title" : "Star Trek"	
            	}
               }
            }'
## Data Modelling in elasticsearch

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjkzODI4NzQsLTEzMjI0MTMyNDUsLTEzMj
Y4ODIzMTksLTIwMzUzMDAwODEsMTE1MTM5MTY4MywtMTExODk5
OTA3Niw5OTYwMzY4NTQsNDAyMjc2NzAsMTUxOTY2NTc1MywxNj
A1MzYxMDE3LDcyMDA4NTQ1NywtMTA0NjcyODI4NiwtMjExNDg3
MDMyMCwtNzQ4MjMyNDY5LC03MjM0NTY3NDgsLTE1OTI5MzMzOF
19
-->