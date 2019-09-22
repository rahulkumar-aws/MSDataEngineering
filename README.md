**1.	Write a query to count the number of products across all orders received by the warehouse system today (the PostgreSQL database).**
```sql	
select count(distinct ord_prd.product_id) from orders ord
inner join order_product ord_prd
on ord.order_id = ord_prd.order_id
where ord.received = NOW()
```




**2.	Given an order_id, how would you find its last GPS coordinates?**	

As given in current data warehouse design order_product table contains 1:Many relationship with order and product.
```text
Order_id	Product_id
O001	P01
O001	P02
O001	P03
```

And in current redis key design there is no order info present. We have to create Key with order_id that will help us to find all GPS coordinates.
Like: delivery: order_id: orders SET order_ids

**3.	What do you think is the most serious problem among these systems, and why? (We are not looking for a specific answer, we want to know what you think is a problem.)**

Some most serious problem among these system:

***Schema design*** is the first concern in these system, if it is not properly design its hard to change and need to do lot of backfills.

***Scalability***, is second concern relational databases mostly scales vertically, we can make a horizontal cluster but complex query joins can’t be distributed and it can make whole system slow.

**4.	Why do you think this fictional company chose Redis for their delivery system, and is it a good choice?**	
	
Redis provide fast insertion and fast O(1) data search capability. In delivery system company has to insert vast amount of data for GPS location, each individual delivery status & address info.

To complete a single delivery app has to query these info in very frequently & redis helps in doing these.
Company can use Memcached but Redis have better scalability & replication functionality over Memcached. Redis also have geospatial data build-in support.




