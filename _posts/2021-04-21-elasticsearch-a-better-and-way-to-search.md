---
layout: post
title: "Elastic search : A better and way to search"
tags:
 -
---

My very first impression of Elastic search was "A cliche NO-SQL database, backed by an organization, which was doing lots of marketing gimmicks to gain attention". Down the line, I did realise that Elastic search was much more than that. Searching document was never been so efficient. Additionally it is based on Apache(OG, GOAT of Free and Open Source Software) Lucene.

Elastic Search is part of `ELK` stack(Elastic Search, Logstash, Kibana)

ELK is `document oriented` database that is optimized for search. It is open-source and distributed(Multiple Node) by default. `ES Cluster` contains one or more nodes for storing data. It contains replicas(For Fault Tolerance) and shard(Single Index spread across different node using shards)

<img src="/as_blog/images/es.png" alt="rxjs image">
### APIs available in Elastic Search

It provide APIs for manipulation and storing Info.

1. `Document Level APIs`: CRUD of document(row)
2. `Index Level APIs:` CRUD of Index(Table)
3. `Cluster Level APIs:` Get info about cluster
4. `Search:` Search for Text using query params and other
5. `Aggregation`

Mapping is the process of defining how a document, and the fields it contains, are stored and indexed. TL:DR; It defines columns and validations

### Seeing List of Indices

```jsx
GET /_cat/indices
HEAD darbhanga //Check if an index name darbhanga exists
```

### Creating Indices

```jsx
PUT darbhanga //Create an index(a.k.a Table for SQL folks out there)
```

### Adding data to indices

```jsx
PUT darbhanga/restaurant/1
{
	"name": "Radhey Radhey",
	"plusPoint": "Ambience",
	"drawback": "Vegetarian food"
},
PUT darbhanga/restaurant/2
{
	"name": "Zaika",
	"plusPoint": "In between Darbhanga and Laheriasarai",
	"drawback": "Food can be bad at times"
}
```

### Document API

Supprts  `Automatic Index Creation`, `Versioning`, `Automatic ID generation`

```jsx
DELETE darbhanga/restaurant/1 //HTTP delete method is used for deleting
//PUT is used for upadating.
```

### Search API

Search APIS are multi-index, multi-type.

```jsx
GET /_all/_search?q=plusPoint:Ambience
```

DSL : Domain Specific language, execute complex queries(branch) by combing simple queries(leaf)

```jsx
//Using DSL to query
POST /darbhanga/_search
{
   "query":{
      "match_all":{}
   }
}

POST /darbhanga*/_search
{
   "query":{
      "match" : {
         "rating":"4.5"
      }
   }
}
```

### Index API

```jsx
GET /darbhanga/_settings //Check Index setting
HEAD darbhanga
GET /_stats
```

### Cat API

```jsx
GET /_cat/indices?v //Verbose
GET /_cat/nodes?h=ip,port //Show only ip and port header
GET _cat/templates?v&s=order:desc,index_patterns //sort
GET /_cat/count?v //Total Number of document
```

### Cluster APIs

```jsx
GET /_nodes/_local // Get Cluster Info
GET /_cluster/health // Get Cluster Health
GET /_cluster/state //state information contains version, master node, other nodes, routing table, metadata and blocks.
GET /_cluster/stats
```

Indexing is the process of adding data to Elasticsearch. When we feed data into Elasticsearch, the data is placed into `Apache Lucene`. This makes sense because Elasticsearch uses the Lucene indexes to store and retrieve its data.

```jsx
curl -XPOST 'localhost:9200/logs/my_app' -H 'Content-Type: application/json' -d'
{
	"timestamp": "2018-01-24 12:34:56",
	"message": "User logged in",
	"user_id": 4,
	"admin": false
}

GET _cat/indices //Gives List of Indices present
```