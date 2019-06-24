---
layout:     post
title:      "PostgreSQL and PostGIS"
subtitle:   " \"\""
date:       2019-04-12 10:00:00
author:     "Ping"
header-img: "img/in-post/postgresql/postgresql.jpg"
catalog: true
tags:
    - Technology
    - Database
    - PostgreSQL
    - PostGIS
---
> PostGIS is an extensional enabling the spatial object and analysis support for PostgreSQL databse.

![schema_facility](/img/in-post/postgresql/facility_schema.jpg)

### Question
Produce a list of facilities with a total revenue less than 1000. Produce an output table consisting of facility name and revenue, sorted by revenue. Remember that there's a different cost for guests and members!

```sql
select facs.name, sum(slots * case
			when memid = 0 then facs.guestcost
			else facs.membercost
		end) as revenue
	from cd.bookings bks
	inner join cd.facilities facs
		on bks.facid = facs.facid
	group by facs.name
	having revenue < 1000
order by revenue;   
```
Solution above doesn't work, gives an error saying **Revenue** doesn't exist. That's because 
unlike some other RDBMSs like SQL Server and MySQL, PostgreSQL doesn't support putting column names in the HAVING 
clause.

So, use solution below instead:

```sql
select name, revenue from (
	select facs.name, sum(case 
				when memid = 0 then slots * facs.guestcost
				else slots * membercost
			end) as revenue
		from cd.bookings bks
		inner join cd.facilities facs
			on bks.facid = facs.facid
		group by facs.name
	) as agg where revenue < 1000
order by revenue;          
```
