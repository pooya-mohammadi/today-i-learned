# Elasticsearch 


## How to solve slow index in elasticsearch or flood stage disk watermark [95%] exceeded on
```commandline
curl -XPUT -H "Content-Type: application/json" http://localhost:9200/_cluster/settings -d '{ "transient": { "cluster.routing.allocation.disk.threshold_enabled": false } }'
curl -XPUT -H "Content-Type: application/json" http://localhost:9200/_all/_settings -d '{"index.blocks.read_only_allow_delete": null}'
```
reference: https://stackoverflow.com/a/63881121/16445477

## How to add local volume to elasticsearch
I tried to change it's uid from 1000 to 1001 (1000 is reserved for linux) using a dockerfile. Nevertheless, it raised several errors.
```commandline
# FROM elasticsearch:8.4.2
# USER root
# RUN groupmod -g 1001 elasticsearch
# RUN usermod -u 1001 -g 1001 elasticsearch
# RUN chown -R elasticsearch /usr/share/elasticsearch
# RUN sed -i -e 's/--userspec=1000/--userspec=1001/g' \
#            -e 's/UID 1000/UID 1001/' \
#            -e 's/chown -R 1000/chown -R 1001/' /usr/local/bin/docker-entrypoint.sh
# RUN chown elasticsearch /usr/local/bin/docker-entrypoint.sh
# USER elasticsearch
```
### Note: Maybe the final error message could have been ignored!!!

## What is error elasticsearch exited unexpectedly 137 docker
This error happends when there is not enough memory available for elasticsearch. Minimum of 2 gigabyte RAM is required!

## How to create a user in elasticsearch
```
docker exec elasticsearch /usr/share/elasticsearch/bin/elasticsearch-users useradd kibana_user -p your-password -r superuser
docker exec elasticsearch /usr/share/elasticsearch/bin/elasticsearch-service-tokens create elastic/kibana kibana-token
# Get the token and set it as env variable for kibana
ELASTICSEARCH_SERVICEACCOUNTTOKEN=<generated-token>
```
