---
title:  "With clause"
date:   2020-11-19
categories: [Database]
tags: [Job search, SQL, Database]
---

It's been 2 months since I graduated from my 26 weeks Bootcamp. Luckily, I have been busy juggling between improving my technical skills and job interviews. Almost all the technical tests I was given during interview processes helped me to boost my knowledge. One of the new concept I have been playing a lot with is **with** clause in SQL. With clause can create subquery blocks which are refered as [Common Table Expressions (CTE)](https://docs.oracle.com/cd/E17952_01/mysql-8.0-en/with.html)

This method is an elegant solution when you need to **retrieve data and produce temporary results** (e.g. transformed data) that can be referred multiple times within a statement. Also, it helps to read and understand better than normal subqueries when used in a complex SQL statement.


Here is an example of a query including CTE:


```
    with

        pickups as
        (
            select
                tpep_pickup_datetime as pickup_time,
                ST_SetSRID(ST_MakePoint(pickup_longitude, pickup_latitude), 4326)
                as pickup_point
            from taxi
        )

    select pickups.*, census.geoid
    from pickups, census_blocks as census
    where ST_Contains(census.geometry, pickups.pickup_point)
    LIMIT 10000;
```

