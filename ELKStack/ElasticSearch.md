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
When we update a document, an new document with incremented _version is created, while the older _version is marked for deletion.








<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgyMjY5NzQ0MSwtMjExNDg3MDMyMCwtNz
Q4MjMyNDY5LC03MjM0NTY3NDgsLTE1OTI5MzMzOF19
-->