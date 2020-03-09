---
layout: post
title:      "Using Indexes to Speed Up Database Queries"
date:       2020-03-09 04:29:41 +0000
permalink:  using_indexes_to_speed_up_database_queries
---


I was recently asked during a technical interview a question regarding how databases worked in the context of finding records with queries. Though I talked about primary and foreign keys, the term I really needed to needed to use was index. I did a little research using the book *Practical SQL* by Anthony DeBarros and learned a couple ideas about databases and indexes.

* Indexes can be added to any column in a database. Whichever column is identified for the primay key will have an index, but you can add it to others. Adding an index does increase the size of the database so you should make sure there is a reason to add one to a column. Also, different databases have different types of indexes so it is a good idea to research what is available in your database and how they work
* One main advantage of adding an index is that is can speed up queries. You can see how this works by comparing queries (for example using "WHERE") on the same database (should be fairly large) with and without an index on the column you are querying. The "EXPLAIN ANALYZE"  keywords when used in a database administration tool such as pgAdmin will show you what type of scan is used and the amount of time. In the example I followed in the book, without an index, the database used a sequential scan to look at each row. With the index, it used a bitmap heap scan which is much faster. It can use this faster search algorithm because in PostgresSQL (which I am using) the default index type is the B-Tree index. This means the database can take advantage of this data structure instead of going through each row of the database. One more reason to study data structures!
