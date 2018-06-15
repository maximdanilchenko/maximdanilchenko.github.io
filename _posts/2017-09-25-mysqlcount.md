---
layout: default
title: "Adding total count to flask-sqlalchemy query results"
permalink: /170925/
---
## Adding total count to _flask-sqlalchemy_ query.


Sometimes, mostly in APIs, we use pagination with SQL ```LIMIT/OFFSET```. 
Usually we need to get count of all available results without ```LIMIT/OFFSET``` filter.
One of the ways is to rerun query, but add ```count()``` function without ```LIMIT/OFFSET```.
But it adds significant overhead because MySQL should do one job twice. 
To optimize it we can use ```FOUND_ROWS()``` information function 
([reference](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_found-rows)). 

So here is a little but useful snippet to add total count to custom sqlalchemy query results:

```python
from collections import namedtuple

QueryResult = namedtuple('QueryResult', ['result', 
                                         'total'])


def with_total(query):
    """ 
    Returns query total rows count 
    without limits with its results 
    """
    result = query.prefix_with(
        'SQL_CALC_FOUND_ROWS').all()
    total = db.session.execute(
        'SELECT FOUND_ROWS();').scalar()
    return QueryResult(result, total)

```
