---
title:  "WITH clause"
date:   2020-11-19
categories: [Database]
tags: [Job search, SQL, Database]
---

Technical tests given during interview processes have been real boosting materials that led me to look for the better solutions to answer the questions. One of the querying techniques I enjoyed using recently is the **WITH** clause. It is used for creating subquery blocks which are known as [Common Table Expressions (CTE).](https://docs.oracle.com/cd/E17952_01/mysql-8.0-en/with.html)

This method is an elegant solution when you need to retrieve data and **produce temporary results (e.g. transformed data) that can be referred to multiple times within a statement**. Also, it enhances the readability of subqueries when used in a complex SQL statement.

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

- As a first step, *tpep_pickup_datetime*, *pickup_longitude*, and *pickup_latitude* columns from a table called *taxi* were retrieved from a PostGIS server.

- A temporary geometry column called *pickup_point* was created by combining *pickup_longitude*, and *pickup_latitude*.

- The result of this subquery was named as *pickups* and it was referred in the following block to produce a final result.

<br>

Multiple **WITH** clauses can be embedded in a single query. The next example is a part of the queries to analyze a series of message records and it contains two **WITH** clauses.

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
	EXTRACT(EPOCH from(sm.message_sent_time - fm.message_sent_time))
        as response_time,
into table customer_courier_conversations
from orders as o
	left join first_messages as fm
		on o.order_id = fm.order_id
	left join second_messages as sm
		on o.order_id = sm.order_id
```

- In the first **WITH** clause, the sender and time of the first message was retrieved temporally as *first_message*.

- In the second **WITH** clause, the time when the second message was sent was retrieved by numbering the order of conversation using **ranking** method and **window** function.

- The final result of the SQL statement was saved as a new table called *customer_courier_conversations*.

<br>

In summary, **CTEs** make it easier to understand subqueries by block separation. And by giving different names to the temporal results, they can be retrieved several times inside a SQL statement.