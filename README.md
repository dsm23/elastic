# Elastic Search Documentation

#### by David Murdoch

## Contents

*[Basics](#basics)*

*[Filters](#queries)*

## Basics

Cluster Health

`GET /_cat/health?v`

Nodes List within cluster
`GET /_cat/nodes?v`

List all Indices
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