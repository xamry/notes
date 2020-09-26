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








