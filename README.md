# Elastic Search Documentation

#### by David Murdoch

## Contents

*[Basics](#basics)*

*[Filters](#filters)*

## Basics

`GET /_cat/health?v`

`GET /_cat/nodes?v`

`GET /_cat/indices?v`

## Queries

```
GET /bank/_search
{
  "query": { "match_all": {} },
  "sort": [
  { "account_number": "asc" }
  ]
}
```
```
GET /bank/_search
{
  "query": { "match_all": {} },
  "size": 1
}
```
```
GET /bank/_search
{
  "query": { "match_all": {} },
  "from": 10,
  "size": 10
}
```
```
GET /bank/_search
{
  "query": { "match_all": {} },
  "sort": { "balance": { "order": "desc" } }
}
```
```
GET /bank/_search
{
  "query": { "match_all": {} },
  "_source": ["account_number", "balance"]
}
```
```
GET /bank/_search
{
  "query": { "match": { "address": "mill" } }
}
```