# Elastic Search Workshop 2019

## Intro - What is ElasticSearch? 🕵🏻‍♀️

You can find API Documentation for [ElasticSearch 5.3 here](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/index.html).


[Link to slides](https://docs.google.com/presentation/d/1PVvW5x0wKULwzrshSyDl92phEJEnWqSwExeXVzcyjfE/edit?usp=sharing)

## Setup Kibana to interact with local ElasticSearch indices

Run `docker-compose -f docker-compose.yml -f ops/docker-compose.es-admin.yml up -d` (from the main KSR repo)

Your local ElasticSearch will run on `localhost:9200` or `localhost:9202`

Visit `localhost:9202/_cat/indices` to verify there are local indices

Go to `localhost:5601` to verify Kibana is running locally

Click on 🔧`DevTools` on the left side navigation in Kibana

🔥Tip: Toggle close the `DevTools` explanation on first visit so the console is in full view

## Get started with some basic ElasticSearch API endpoints

To start playing around with Kibana, run these commands and hit the green ▶️ button to make a request.

`GET _cat/indices` - [gets all indices](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/cat-indices.html)


`GET <name of index>` - [gets basic info on index](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/indices-get-index.html)

🔥Tip: Pick an index from your index list that starts with `development_es5*`

`GET development_es5_users_2019_11_29_16_10_25/_search` - returns all documents in index 

📝: We'll come back to `_search` a lot more later

`PUT my_new_index` - [creates new index](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/indices-create-index.html) 

🔥Tip: Verify your index was created by running `GET _cat/indices` again

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

"my_new_pet_index" is the name of your index and "dogs" is the type name

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
}
```

#### Mappings
ElasticSearch also automatically creates mappings.

Run `GET my_new_pet_index/_mapping` to see what mappings were created for your index.

Add a new document to your index with a new field and then check  the mappings again.

```
POST my_new_pet_index/dogs
{
  "name": "Ashley",
  "age": 4,
  "birthdate": "2019-03-22",
  "my_new_field": "hello"
}
```

More likely, you'll want to create your own mapping when you create your index to have more control over fields and types.

```
PUT my_favorite_movies
{
  "mappings": {
    "doc": {
      "properties": {
        "name": {
          "type": "text"
        }
      }
    }
  }
}
```

In the Kickstarter app, we create mappings for all of our indices and ensure that a document won't be added with fields not in the mapping. 

`GET development_es5_backings*/_mapping`

#### Deleting indices
`DELETE my_new_pet_index`

## Search and the Query DSL

#### Setup

Using ElasticSearch's [Bulk API](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/docs-bulk.html), create a new index with multiple documents to build a searchable index.

Copy and paste the fake restaurant review data [here](https://raw.githubusercontent.com/kickstarter/elastic-search-workshop/master/resources/bulk_index_data.txt) and add it to the body of your bulk request.

```
POST fake_restaurants/reviews/_bulk
{"index":{}}
{"name":"Belly Steakhouse","description":"Our mission has been to help people achieve their health and wellness goals. though weve changed over the years, our values have remained the same.","cuisine":"Burgers","review":"Staff was very accommodating but the chef were no nonsense. The ambiance is clean and tranquil which is perfect if youre looking to have a conversation with a date or a friend.","city":"Luettgenport","created_at":"2019-07-16","delivery":false}
{"index":{}}
{"name":"Belly Dragon","description":"To achieve and maintain such distinction in food and wine, service, atmosphere and setting that the restaurant gains a first class reputation for gastronomy, gracious and informed hospitality, comfort and beauty which draws new and repeat customers year after year. To achieve the above whilst upholding staff policies and practices which promote a fair and positive working environment. To be aware of and act on our responsibilities as a good corporate citizen to  provide a safe, clean and attractive place for guests to enjoy and for employees to work in - ensure ecologically sound management practices at the restaurant and in our surrounding gardens and woods - undertake meaningful involvement of Restaurant Les Fougères in selected charitable activities in our community and region.","cuisine":"Brazilian","review":"This particular location like the many other restaurants down the block has ample seating and a second floor.","city":"East Lilia","created_at":"2018-07-26","delivery":false}
...
...
```

#### Queries
`match_all` is the default search. 

`GET fake_restaurants/_search`

is the same as
```
GET fake_restaurants/_search
{
  "query": {
    "match_all": {}
  }
}
``` 
---
`match`

`multi_match`
`match_phrase` - something where in match we get back a lot of  hits and match_phrase hones in on it more

keyword filtering? 
"chocolate drizzled" -
command f  to look at your hits 

-----
TKTKTK
Day 2 roughly 
bool queries

#### Aggregations

## Explore a KSR Projects Index

## Extro
glossary/vocab 
other things to think a bout
Scores 
How to make certain things more relevant / score bias
analyzers?
