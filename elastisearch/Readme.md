# Elasticsearch 


## How to solve slow index in elasticsearch or flood stage disk watermark [95%] exceeded on
```commandline
curl -XPUT -H "Content-Type: application/json" http://localhost:9200/_cluster/settings -d '{ "transient": { "cluster.routing.allocation.disk.threshold_enabled": false } }'
curl -XPUT -H "Content-Type: application/json" http://localhost:9200/_all/_settings -d '{"index.blocks.read_only_allow_delete": null}'
```
reference: https://stackoverflow.com/a/63881121/16445477
