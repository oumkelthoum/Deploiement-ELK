## Definition ELK
- Qu'est-ce qu'un Elk ?
ELK est un outil d'analyse de logs composé de 3 logiciels : Elasticsearch, Logstash et Kibana.
 Elasticsearch extrait les données, Logstash normalise les données temporelles et Kibana est un outil de visualisation.


- Install ELK Stack (Elasticsearch, Logstash, and Kibana) on Ubuntu 18.04 

-- Install Elasticsearch  

`sudo wget --directory-prefix=/opt/ https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.6.1-amd64.deb`
`sudo dpkg -i /opt/elasticsearch*.deb`
`sudo apt-get install elasticsearch`
## edit /etc/elasticsearch/elasticsearch.yml
#host.name + master
#network.host: 0.0.0.0
#discovery.seed_hosts: ["127.0.0.1", "@ip de la machine"]


## edit /etc/elasticsearch/jvm.options

adding the lines :
- Xms represents the initial size of total heap space
- Xmx represents the maximum size of total heap space

-Xms512m
-Xmx512m

- Then : 
 `systemctl enable elasticsearch`
 `systemctl start elasticsearch`

# Test Elasticsearch

curl -X GET "localhost:9200" 

--  Install Kibana

`sudo apt-get install kibana`

- Configure kibana
# edit sudo nano /etc/kibana/kibana.yml

 server.port: 5601
 server.host: "localhost"
 elasticsearch.hosts: ["http://localhost:9200"]

`sudo systemctl start kibana`
`sudo systemctl enable kibana`

 # Allow Traffic on Port 5601
`sudo ufw allow 5601/tcp`

 # Test Kibana

 To access Kibana, open a web browser and browse to the following address : http://localhost:5601

 -- Install Logstash

`sudo apt-get install logstash`


- Configure Logstash

Logstash est une partie hautement personnalisable de la pile ELK. Une fois installé, configurez ses pipelines INPUT, FILTERS et OUTPUT en fonction de votre propre cas d'utilisation.

 
`sudo apt-get install logstash`
`sudo systemctl start logstash`
`sudo systemctl enable logstash`
`sudo systemctl status logstash`



- Install Filebeat

Filebeat est un plugin léger utilisé pour collecter et envoyer des fichiers journaux. C'est le module Beats le plus couramment utilisé. L'un des principaux avantages de Filebeat est qu'il ralentit son rythme si le service Logstash est submergé de données

|``sudo apt-get install filebeat``


- Configure Filebeat 

Filebeat, par défaut, envoie des données à Elasticsearch. Filebeat peut également être configuré pour envoyer des données d'événement à Logstash.

1. To configure this, edit the filebeat.yml configuration file:

``sudo nano /etc/filebeat/filebeat.yml``

2. Under the Elasticsearch output section, comment out the following lines:

# output.elasticsearch:
   # Array of hosts to connect to.
   # hosts: ["localhost:9200"]

3. Under the Logstash output section, remove the hash sign (#) in the following two lines:

# output.logstash
     # hosts: ["localhost:5044"]

It should look like this:

output.logstash
     hosts: ["localhost:5044"]


Example of import data in kibana 

- First off all 
  * Create a file #test.conf under the directory ( /usr/share/logstash/bin) the context is :


``` 
input {
file {
path => "/home/kelthem/Desktop/diabetes.csv"
start_position => "beginning"
}
}
filter {
csv {
separator => ","
columns => [ "C1",..... ,"Cn" ]
}
}
output {
elasticsearch { 
hosts => ["localhost:9200"] 
index => "name of the index "
}
}

```
After executing the following command to launch logstash which allows injection into elasticsearch:

`sudo bin/logstash -f config/test.conf`

Verify if the new pattern was created with the following command: 

`` curl -XGET http://localhost:9200/_cat/indices?v ``

* In the kibana daschboard 
Home -> Stack management -> Management -> Index patterns 

Choose the index pattern in the kibana dashboard 

Then dashboard -> create a new -> create a visualization -> choose the index pattern 





