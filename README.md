# Elastic Search Query Commands

#### by David Murdoch

## Contents

**[Basics](#basics)**

**[Queries](#queries)**

## Basics

Cluster Health

`GET /_cat/health?v`

Nodes List within cluster
`GET /_cat/nodes?v`

List all Indices
`GET /_cat/indices?v`

https://www.elastic.co/guide/en/elasticsearch/reference/current/_introducing_the_query_language.html

## Queries

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