# Elastic Search Workshop 2019

### Intro - What is ElasticSearch? 🕵🏻‍♀️
---

[Link to slides]()


### Setup Kibana locally to interact with local ElasticSearch indices
---
1. Run `docker-compose -f docker-compose.yml -f ops/docker-compose.es-admin.yml up -d`
2. Your local ElasticSearch will run on `localhost:9200` or `localhost:9202`
3. You can visit `localhost:9202/_cat/indices` to verify there are local indices
4. Go to `localhost:5601` to verify Kibana is running locally
5. Click on 🔧`DevTools` on the left side navigation in Kibana 


### Get started with some basic ElasticSearch API endpoints
---
To start playing around with Kibana, you can run these commands and hit the green ▶️ button.

`GET _cat/indices` - [gets all indices](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/cat-indices.html)

`GET /<name of index>` - [gets basic info on index](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/indices-get-index.html)

`GET /<name of index>/_search` - returns all documents in index

TKTK add two more


### Create your own index

### Search and the query DSL

### Exploring a KSR Index