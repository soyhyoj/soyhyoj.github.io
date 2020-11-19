---
title:  "With clause"
date:   2020-11-19
categories: [Database]
tags: [Job search, SQL, Database]
---

Almost all the technical tests I was given during interview processes helped me to boost my knowledge by looking for better solutions. One of the new concept I have been playing a lot with is **WITH** clause in SQL. With clause is used for creating subquery blocks which are refered as [Common Table Expressions (CTE)](https://docs.oracle.com/cd/E17952_01/mysql-8.0-en/with.html)

This method is an elegant solution when you need to retrieve data and **produce temporary results (e.g. transformed data) that can be referred multiple times within a statement**. Also, it helps to read and understand better subqueries when used in a complex SQL statement.

Here is an example of a query including CTE from my recent [geospatial analysis](https://github.com/soyhyoj/GeospatialAnalysis_NYtaxi).:


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

- As a first step, I retrieved *tpep_pickup_datetime*, *pickup_longitude*, and *pickup_latitude* columns from a table called *taxi* saved in a PostGIS server.

- Inside this subqquery, a new temporary geometry column called *pickup_point* was created by combining *pickup_longitude*, and *pickup_latitude*.

- The result of this subquery was named as *pickups* and it was referred in the following block to produce a final result.

<br>

Another example I created is practical when you have a series of message records and wants to identify
    1. Who was the first message sender
    2. When was the time when the first message was sent
    3. When was the second message was sent

```
with
first_messages as
(
	select
		order_id,
		message_sent_time,
		case when from_id = courier_id then 'Courier'
		else 'Customer'
		end as message_sender
	from customer_courier_chat_messages 
	where message_sent_time in
	(
		select min(message_sent_time)
		from customer_courier_chat_messages
		group by order_id
	)
),

second_messages as
(
	with message_order as
	(
		select
			order_id,
			message_sent_time,
			rank() over (partition by order_id order by message_sent_time) as message_n
		from customer_courier_chat_messages 
	)
	select
		order_id,
		message_sent_time
	from message_order
	where message_n = 2
)

select  
	o.order_id,
	o.city_code,
	fm.message_sender as first_message_sender,
	fm.message_sent_time as first_message_time,
	EXTRACT(EPOCH from(sm.message_sent_time - fm.message_sent_time)) as response_time,
into table customer_courier_conversations
from orders as o
	left join first_messages as fm
		on o.order_id = fm.order_id
	left join second_messages as sm
		on o.order_id = sm.order_id
```

- In the first WITH clause, the first sender and message time of each conversation was retrieved as a temporal table called *first_message*

- In the second WITH clause, the second message time was retrieved by numbering the order of conversation using **ranking** method and **window** function.

<br>

<br>