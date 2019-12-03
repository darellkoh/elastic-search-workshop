# Elastic Search Workshop 2019

## Intro - What is ElasticSearch? 🕵🏻‍♀️

[Link to slides]()

## Setup Kibana to interact with local ElasticSearch indices

Run `docker-compose -f docker-compose.yml -f ops/docker-compose.es-admin.yml up -d`

Your local ElasticSearch will run on `localhost:9200` or `localhost:9202`

Visit `localhost:9202/_cat/indices` to verify there are local indices

Go to `localhost:5601` to verify Kibana is running locally

Click on 🔧`DevTools` on the left side navigation in Kibana

## Get started with some basic ElasticSearch API endpoints

To start playing around with Kibana, run these commands and hit the green ▶️ button to make a request.

`GET _cat/indices` - [gets all indices](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/cat-indices.html)

`GET <name of index>` - [gets basic info on index](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/indices-get-index.html)

`GET <name of index>/_search` - returns all documents in index

`PUT <name of new index>` - [creates new index](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/indices-create-index.html)

## Create your own index

#### Creating documents

ElasticSearch [automatically creates an index](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/docs-index_.html#index-creation) when a new document is created for an index that doesn't exist yet:

```
POST my_new_pet_index/dogs
{
  "name": "Lulu",
  "age": 2,
  "birthdate": "2019-01-03"
}
```

Run `GET my_new_pet_index` to verify your new index exists.

Create a new document and specify an id:

```
POST my_new_pet_index/dogs/1
{
  "name": "Teddy",
  "age": 3,
  "birthdate": "2019-03-22"
}
```

Run both requests again and take note of the `created` property in the response.

Run `GET my_new_pet_index/_search` to see how many documents are in the index.

#### Updating documents

[Update a document](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/docs-update.html) by making a `PUT` request and specifying an id to update in the params:

```
PUT my_new_pet_index/dogs/1
{
  "name": "Theodore",
  "age": 3,
  "birthdate": "2019-03-22",
  "a_new_field": true
}
```

#### Mappings

#### Deleting indices

## Search and the Query DSL

#### Setup

Using ElasticSearch's [Bulk API](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/docs-bulk.html), create a new index with multiple documents to build a searchable index.

Copy and paste the fake restaurant review data [here](https://github.com/kickstarter/elastic-search-workshop/blob/master/resources/bulk_index_data.md) and add it to the body of your bulk request.

```
POST fake_restaurants/_reviews/_bulk
{"index":{}}
{"name":"Belly Steakhouse","description":"Our mission has been to help people achieve their health and wellness goals. though weve changed over the years, our values have remained the same.","cuisine":"Burgers","review":"Staff was very accommodating but the chef were no nonsense. The ambiance is clean and tranquil which is perfect if youre looking to have a conversation with a date or a friend.","city":"Luettgenport","created_at":"2019-07-16","delivery":false}
{"index":{}}
{"name":"Belly Dragon","description":"To achieve and maintain such distinction in food and wine, service, atmosphere and setting that the restaurant gains a first class reputation for gastronomy, gracious and informed hospitality, comfort and beauty which draws new and repeat customers year after year. To achieve the above whilst upholding staff policies and practices which promote a fair and positive working environment. To be aware of and act on our responsibilities as a good corporate citizen to  provide a safe, clean and attractive place for guests to enjoy and for employees to work in - ensure ecologically sound management practices at the restaurant and in our surrounding gardens and woods - undertake meaningful involvement of Restaurant Les Fougères in selected charitable activities in our community and region.","cuisine":"Brazilian","review":"This particular location like the many other restaurants down the block has ample seating and a second floor.","city":"East Lilia","created_at":"2018-07-26","delivery":false}
...
...
```

#### Queries

#### Aggregations

## Explore a KSR Index
