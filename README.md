# Elastic Search Query Commands

#### by David Murdoch

## Contents

* [Basics](#basics)

* [Queries](#queries)

	* [URI Search](#uri-search)

* [Java](#java)

## Basics

Cluster Health

```GET /_cat/health?v```

Nodes List within cluster

```GET /_cat/nodes?v```

List all Indices

```GET /_cat/indices?v```

HTTP REQUESTS:

GET,POST, PUT, DELETE

GET is the most used for queries

https://www.elastic.co/guide/en/elasticsearch/reference/current/_introducing_the_query_language.html

how to add a json file to an index

```
curl -H "Content-Type: application/json" -XPOST 'localhost:9200/bank/account/_bulk?pretty&refresh' --data-binary "@accounts.json
```

https://www.elastic.co/guide/en/elasticsearch/reference/index.html

## Queries

#### URI Search

```javascript
GET bank/_search?q=gender=M
```

`GET _all`

`GET /customer/external/1?pretty`

where pretty is the name of an index

match_all query is simply a search for all documents in the specified index.
```javascript
GET /bank/_search
{
  "query": { "match_all": {} },
  "sort": [
  { "account_number": "asc" }
  ]
}
```
where bank is the index

```javascript
GET /bank/_search
{
  "query": { "match_all": {} },
  "size": 1
}
```
```javascript
GET /bank/_search
{
  "query": { "match_all": {} },
  "from": 10,
  "size": 10
}
```
```javascript
GET /bank/_search
{
  "query": { "match_all": {} },
  "sort": { "balance": { "order": "desc" } }
}
```
```javascript
GET /bank/_search
{
  "query": { "match_all": {} },
  "_source": ["account_number", "balance"]
}
```
```javascript
GET /bank/_search
{
  "query": { "match": { "address": "mill" } }
}
```

Two match queries and returns all accounts containing "mill" and "lane"
```javascript
GET /bank/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }
}
```

Two match queries and returns all accounts containing neither "mill" and "lane"
```javascript
GET /bank/_search
{
  "query": {
    "bool": {
      "must_not": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }
}
```

#### Agregations

```javascript
GET /bank/_search
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}
```

equivalent to 
```sql
SELECT state, COUNT(*) FROM bank GROUP BY state ORDER BY COUNT(*) DESC
```

```javascript

```

|  ||
|:---:|:---:|
| gte  | Greater than or equal to |
| gt | Greater than|
| lte | Less than or equal to|
| lt | Less than|

```javascript
GET /bank/_search
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword"
      },
      "aggs": {
        "average_balance": {
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}
```

equivalent to 
```sql
SELECT state, COUNT(*), AVG(balance) FROM bank GROUP BY state ORDER BY COUNT(*) DESC
```

all of the following are in a "bool"
Query DSL | Operand
|:---:|:---|
must | AND
must_not | NOT
should | OR

important terms: query, filter, aggr

```javascript
GET /bank/_search
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword",
        "order": {
          "average_balance": "desc"
        }
      },
      "aggs": {
        "average_balance": {
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}
```

## Java

Does not involve Pages and PageObject

Placed in the Step Libraries folder
```java
static Node node;
static Client client;

public static void setup(){

	node = nodeBuilder()
		.settings(Settings.builder()
			.put("path.home", "/"))
		.clusterName("elasticsearch").client(true).node();
	client = node.client();

}
```
https://www.elastic.co/guide/en/elasticsearch/client/java-api/2.0/node-client.html

No need for @Steps
```java
	ElasticSearchSteps elasticSearchSteps;
    SearchResponse searchResponse;
    SearchResponse getAllEntriesResponse;
    DeleteResponse deleteResponse;
    IndexResponse indexResponse;
```
[SERVICE_UNAVAILABLE/1/state not recovered / initialized]

launch elasticsearch.bat

This way it does not require a path home

can also install elasticsearch with a msi file but this requires changing the path home

`size:` defaults to 10



```java
static Node node;
static Client client;

public static void setup(){

	node = nodeBuilder()
		.settings(Settings.builder()
		.put("path.home", "/"))
		.clusterName("elasticsearch").client(true).node();
	client = node.client();


}
```
<elasticsearch.version>5.6.1</elasticsearch.version>

<dependency>
    <groupId>org.elasticsearch.client</groupId>
    <artifactId>transport</artifactId>
    <version>5.0.0-beta1</version>
</dependency>