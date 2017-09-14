# Elastic Search Documentation

#### by David Murdoch

## Contents

*[Basics](#basics)*

*[Filters](#filters)*

## Basics

`GET /_cat/health?v`

`GET /_cat/nodes?v`

`GET /_cat/indices?v`

## Filters

`GET /bank/_search

{

  "query": { "match_all": {} },

  "sort": [

  { "account_number": "asc" }

  ]

}`