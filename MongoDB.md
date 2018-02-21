# MongoDB basics

## tl;dr

`MongoDB` is a `NoSQL` Database that can store `documents`, that looks like a JSON. You can query to get JSON-like documents NOT by making up SQLs, but by calling methods from libraries to get documents.

## Documents

`Document`s are basic blocks in MongoDB, like `row`s in relational DBs.

`Document`s seem like a json document. It:
- has key-value pair
- can have nested documents, i.e. dicts in value
- can have arrays

![mongodb documents](https://docs.mongodb.com/manual/_images/crud-annotated-document.bakedsvg.svg)

## _id

When you create a document, MongoDB will silently add one more field for you, named `_id`. This field is unique, indexed, and you can query items by `_id` safely.

Type of `_id` is not `String`, but a special `ObjectId`. You can losslessly convert it from and to `String`, and the converted string is URL-safe. You can use this string in RESTful APIs.

## Databases and Collections

A Database is a number of collections, and a collection is a set of documents.

You typically use a database for a project, and place different types of data into different collections.

Documents in a collection are free-formed, meaning a `collection` of documents are not necessary of the same shape. However it is recommended to place documents of different purpose into different collections.

for example: 
```
database MyProject
- collection Users
    {
        '_id': ObjectId('xxxxxxxxxxxxxxxx'),
        'name':'kinomoto sakura',
        'age': 14,
        'items': ['wind', 'aqua']
    }
- collection Items
    {
        '_id': ObjectId('xxxxxxx'),
        'name': 'wind',
        'story': 'a long story'
    }
```

## Indexes

When you query a collection, the whole collection is scanned. It is slow. But you can add index to make it better.

You can add Index to a field in a collection, then all documents in this collection with such field is indexed. After construction of index, you can make query and find it faster. 

Indexes are transparent to query clients, only faster.

Indexes require `O(n)` more spaces, and reduce query time from `O(n)` to `O(log(count(values of such field)))`


## Roles

You may want some security, forbid strangers or interns from accessing or modifying your data. MongoDB can do that.

By default, this system is disabled, and anyone can do everything. Easy to use but dangerous.

If you enabled this system (called `Role-Based Access Control`), your actions are checked with your user permission.

There are many `action`s, like `find` and `createCollection`. 

There are a bunch of `role`s, each role are granted a list of allowed `action`s.

`Role`s can inherit from other `role`s. There are system built-in roles, but you can create your own role.

You are a `user`. A user can be assigned a list of `role`s. Your action is allowed iff this action is allowed in one of your roles.

## More

MongoDB is strong in distribution. You can have a distributed MongoDB in multiple machines, and have better performance and safety. This is however out of scope of this page.