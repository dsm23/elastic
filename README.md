# Elastic Search Query Commands

#### by David Murdoch

## Contents

*[1. Basics](#basics)*

*[2. Queries](#queries)*

## 1. Basics

Cluster Health

`GET /_cat/health?v`

Nodes List within cluster
`GET /_cat/nodes?v`

List all Indices
`GET /_cat/indices?v`

## 2. Queries

`GET /customer/external/1?pretty`

where pretty is the name of an index

```javascript
GET /bank/_search
{
  "query": { "match_all": {} },
  "sort": [
  { "account_number": "asc" }
  ]
}
```
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