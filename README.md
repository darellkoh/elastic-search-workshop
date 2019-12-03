# Elastic Search Workshop 2019

## Intro - What is ElasticSearch? 🕵🏻‍♀️

[Link to slides]()

## Setup Kibana locally to interact with local ElasticSearch indices

1. Run `docker-compose -f docker-compose.yml -f ops/docker-compose.es-admin.yml up -d`
2. Your local ElasticSearch will run on `localhost:9200` or `localhost:9202`
3. Visit `localhost:9202/_cat/indices` to verify there are local indices
4. Go to `localhost:5601` to verify Kibana is running locally
5. Click on 🔧`DevTools` on the left side navigation in Kibana

## Get started with some basic ElasticSearch API endpoints

To start playing around with Kibana, you can run these commands and hit the green ▶️ button.

`GET _cat/indices` - [gets all indices](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/cat-indices.html)

`GET /<name of index>` - [gets basic info on index](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/indices-get-index.html)

`GET /<name of index>/_search` - returns all documents in index

TKTK add two more

## Create your own index

1. Create a new document
2. Update a document

## Search and the Query DSL

#### Setup

Using the ElasticSearch [Bulk API](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/docs-bulk.html), create a new index with many documents so that we can begin playing with search queries.

Copy and paste the fake restaurant review data [here](https://github.com/kickstarter/elastic-search-workshop/blob/master/resources/bulk_index_data.md) and paste it into the body of your bulk request.

```
POST fake_restaurants/_reviews/_bulk
  ...
  ...
  {"index":{}}
  {"name":"Belly Steakhouse","description":"Our mission has been to help people achieve their health and wellness goals. though weve changed over the years, our values have remained the same.","cuisine":"Burgers","review":"Staff was very accommodating but the chef were no nonsense. The ambiance is clean and tranquil which is perfect if youre looking to have a conversation with a date or a friend.","city":"Luettgenport","created_at":"2019-07-16","delivery":false}
  ...
  ...
```

#### Queries

#### Aggregations

## Explore a KSR Index
