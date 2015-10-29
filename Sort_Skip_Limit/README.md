##Sort,Skip and Limit
Chris Zeng, Oct 25 2015

Regardless of the sequence of sort(), skip() and limit() functions placement, Pymongo will be executed in a fixed order:

* sort 
* skip 
* limit

For example, given we

```
{ "_id" : 1, "price" : 110 }
{ "_id" : 2, "price" : 53 }
{ "_id" : 3, "price" : 69 }
{ "_id" : 4, "price" : 220 }
```

```
output = things.find().sort( 'price', pymongo.DESCENDING ).skip( 3 ).limit( 1 )
```

will return exactly the same query result as 

```
output = things.find().skip( 3 ).limit( 1 ).sort( 'price', pymongo.DESCENDING )
```

which finally returns:
```
{ "_id" : 2, "price" : 53 }
```

###sort order syntax in Pymongo (vs mongo shell)


Note the `pymongo.DESCENDING` parameter in Pymongo, is different from that of the mongo shell `-1` for descending,
and `1` ascending.

###sort using multiple orders
Needs an array of tuples 

```
cursor = cursor.sort([('student_id',pymongo.ASCENDING),
('score',pymongo.DESCENDING)])
```