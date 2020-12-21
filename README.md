# playELK

[Usage](https://elk-docker.readthedocs.io/#usage)

Run a container from the image with the following command:

$ sudo docker run -p 5601:5601 -p 9200:9200 -p 5044:5044 -it --name elk sebp/elk

This command publishes the following ports, which are needed for proper operation of the ELK stack:

5601 (Kibana web interface).

9200 (Elasticsearch JSON interface).

5044 (Logstash Beats interface, receives logs from Beats such as Filebeat – see the Forwarding logs with Filebeat section).

The image exposes (but does not publish):

Elasticsearch's transport interface on port 9300. Use the -p 9300:9300 option with the docker command above to publish it. This transport interface is notably used by Elasticsearch's Java client API, and to run Elasticsearch in a cluster.

Logstash's monitoring API on port 9600. Use the -p 9600:9600 option with the docker command above to publish it.

$ sudo docker-compose up

$ docker run -d \
  --name=filebeat \
  --user=root \
  --volume="$(pwd)/filebeat.docker.yml:/usr/share/filebeat/filebeat.yml:ro" \
  --volume="/var/lib/docker/containers:/var/lib/docker/containers:ro" \
  --volume="/var/run/docker.sock:/var/run/docker.sock:ro" \
  --volume="$(pwd)/csv/:/var/log/"
  docker.elastic.co/beats/filebeat:7.10.1 filebeat -e -strict.perms=false \
  -E output.elasticsearch.hosts=["elasticsearch:9200"]

