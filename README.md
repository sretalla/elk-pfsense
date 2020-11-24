# elk-pfsense
This repo is to store the setup for an ELK docker container based on sebp/elk:latest (version 7+) to get logs from Pfsense 2.4 and generate a dashboard to vizualize your logs.

Run the container with ports and volumes like this:\
docker run -d  --name elk-pfsense \
-p 5140:5140 \
-p 5141:5141/udp \
-p 9200:9200 \
-p 5044:5044 \
-p 5601:5610 \
-v elastic-config:/etc/elasticsearch:ro \
-v elastic-data:/var/lib/elasticsearch:rw \
-v logstash-config:/etc/logstash:ro \
-v kibana-config:/opt/kibana/config:ro \
sebp/elk:latest

Then once the container runs, go to the app: http://docker-host:5601/ and create an index called logstash-* and then go to the dev console under: http://docker-host:5601/app/dev_tools#/console
Copy the text from geohash index in the root and hit the play button.

Then you have the data from your pfsense 2.4 install ready to go by going to Status|System Logs|Settings, then Enable remote logging and list docker-host:5141 as one of the remote servers (make sure you also enable at least firewall in the list below that).

max virtual memory areas vm.max_map_count [65530] likely too low, increase to at least [262144] means that the host's limits on mmap counts must be set to at least 262144\


