---
layout: post
title: Powerup your searches
categories: [Development, PHP, Search, ElasticSearch]
tags: [PHP, Search, ElasticSearch, Fucking Awesome]
---
# ElasticSearch - Powerup your searches!

## First things first
_ElasticSearch_ is a _flexible and powerful open source, distributed real-time
search and analytics engine for the cloud_

In other _languages_, __ES__ is fucking awesome!

## Indexing data

JSON Documents are stored into an __Index__ in a given __Type__.

We can think that an __Index__ is something like a _table_ (NEVER, NEVER SAY THAT.. just imagine, please) and this table can have different data structure between its objects.

Not necessarily, a __Type__ is attached to a schema, once __ES__ can work with _Schema less_

__ES__ has a cool REST API, and we will play with it to store our new _data_ into a _Automobiles_ index and a _Car_ type

Given that we have the following document:

```php
{
    "manufacturer" : "Buick",
    "model" : "Verano",
    "color" : "Silver"
}
```

Let's use cURL to store this _marvelous_ car into its index

```php
$ curl -XPUT 'http://localhost:9200/automobiles/car/1' -d '{
    "manufacturer" : "Buick",
    "model" : "Verano",
    "color" : "Silver"
}'
```

Following the _Type_ idea, we can have a Truck _type_, Bus _type_, __Whatever__ _type_.


## Automatic index id

We can let elasticsearch to create the index __id__ by it self

```php
$ curl -XPOST 'http://localhost:9200/automobiles/car' -d '{
    "manufacturer" : "Buick",
    "model" : "Encore",
    "color" : "Black"
}'
```

## Versioning

And I can even versioning an _index_ giving to my _Verano_ the _blue color_

```php
$ curl -XPUT 'http://localhost:9200/automobiles/car/1?version=2' -d '{
    "color" : "Blue"
}'
```

## TTL

A document can be indexed with a TTL associated with it

```php
$ curl -XPUT 'http://localhost:9200/automobiles/car?ttl=1d' -d '{
    "manufacturer" : "Chevrolet",
    "model" : "Impala",
    "color" : "Black"
}'
```

## Nested Objects

Following the idea that _I CAN map_ a Document, but _I DON'T NEED_, we will create a nested object without mapping to perform a nested object search

```php
$ curl -XPOST 'http://localhost:9200/users/user' -d '{
    "name": "Kinn",
    "profile": {
    	"links": {
    		"github": "http://github.com/kinncj",
    		"about_me": "http://about.me/kinncj",
    		"blog": "http://kinncj.eu"
    	},
    	"address": {
    		"country": "canada",
    		"city": "toronto"
    	}
	}
}'

$ curl -XPOST 'http://localhost:9200/users/user' -d '{
    "name": "Chimbinha",
    "profile": {
    	"links": {
    		"github": "http://github.com/some_user",
    		"about_me": "http://about.me/some_user",
    		"blog": "http://some.blog.cc"
    	},
    	"address": {
    		"country": "canada",
    		"city": "toronto"
    	}
	}
}'

$ curl -XPOST 'http://localhost:9200/users/user' -d '{
    "name": "Manolo",
    "profile": {
    	"links": {
    		"github": "http://github.com/another_user",
    		"about_me": "http://about.me/another_user",
    		"blog": "http://another.blog.cc"
    	},
    	"address": {
    		"country": "Brazil",
    		"city": "Curitiba"
    	}
	}
}'
```

## Searching

Now, we will be able to perform a search in a node of the Nested object _WITHOUT MAPPING_
Isn't it fucking crazy? Yeah, it it!

```php
$ curl -XPOST 'http://localhost:9200/users/user/_search' -d '{
    "query": {
        "filtered": {
            "query": {
                "match_all": {}
            },
            "filter": {
                "and": [
                    {
                        "term": {
                            "profile.address.country": "canada"
                        }
                    },
                    {
                        "term": {
                            "profile.address.city": "toronto"
                        }
                    }
                ]
            }
        }
    }
}'
```
In this query, we are telling to __ES__ to search for _All documents_ filtered by _profile.country_ and _profile.city_


## PHP

The integration with PHP is kind easy, since the query is made by a JSON, we just need to create a stdClass and send to __ES__

To make things easy, there's a __cool__ _QueryBuilder_ for PHP that you can find [here](https://packagist.org/packages/phpfluent/elastic-query-builder)

The sintax is kinda __cool__, and you can check below:

```php
  $query = new Query;
  $query->query()->filtered()->query()->match_all(new \stdClass);
  $query->query()->filtered()->filter()->and(
    array(
      new Term("profile.address.country", "canada"),
      new Term("profile.address.city", "toronto")
    )
  );
  ```

  And this will generate the same JSON that we have above.

  Using the __QueryBuilder__ with [Guzzle](http://docs.guzzlephp.org/en/latest/), you'll have the minimun effort to query __ES__ Like a boss!

  ```php
  $query = new Query;
  $query->query()->filtered()->query()->match_all(new \stdClass);
  $query->query()->filtered()->filter()->and(
    array(
      new Term("profile.address.country", "canada"),
      new Term("profile.address.city", "toronto")
    )
  );

  $client  = new Client;
  $request = $client->post('http://localhost:9200/users/user/_search', null, (string) $query);
  $data    = $request->send()->json();

  var_dump($data);
```

## Who is using it?

Me! hahaha

Not only me, but __cool__ companies around the _Globe_, as:

 * FourSquare - 50 million venues in real time
 * SoundCloud - 180 million people searching online audio
 * GitHub     - 20TB of Data using ElasticSearch, including 1.3 billion files and 130 billion lines of code
 * etc

 So, are you gonna spend your time tunning and enhancing queries on your Solr/Sphinx/WhatEver? Or will you try to give a chance to __ES__ as GitHub, FourSquare and other _cool companies_ did?

 ## Whats comming up?

 Maybe in the next time, I'll try to talk a little about GeoLocation query, Range query, _more like this_ query and other _cool_ features of __ES__

 Thanks!
