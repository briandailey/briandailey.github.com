---
layout: post
title: "Amazon Redshift - What You Need To Know"
description: ""
category: 
tags: [amazon, redshift, sql, database]
---
{% include JB/setup %}

Stratasan, a company I co-founded in 2010, moved from PostgreSQL to Amazon
Redshift in 2013. Now that we've migrated most of our data to the platform, I
thought it would be useful to others out there if I summarized some of our
experiences during the transition (much like [others have
done](http://nerds.airbnb.com/redshift-performance-cost) before us).


### What Is Amazon Redshift?

Amazon Redshift is a managed database platform that looks, smells, and tastes
an awful lot like PostgreSQL 8. That said, it isn't really PostgreSQL. Before
Amazon released Redshift, a company called
[ParAccel](http://www.zdnet.com/amazon-redshift-paraccel-in-costly-appliances-out-7000008111/)
had built a managed database platform that was designed for analytics. What set
it appart is that it was originally touted to run well on commodity hardware.
(Source: [Wikipedia](http://en.wikipedia.org/wiki/ParAccel)) Amazon made a
significant investment in the company, and used their platform to create
Redshift.

Redshift is built for analytics. It's a columnar data store, so it's intended
to return fast results for aggregations (SUM, AVG, COUNT, etc). Single-store
lookups are, of course, much slower.

### Why I Like Redshift

We checked out Hadoop and Elasticsearch prior to using Redshift. For various
reasons, neither fit our need very well. We needed a way to handle data in
various shapes and sizes without spending a ton of time on pre-processing. As a
Python shop, we didn't want to spend an inordinate amount of time learning Java
or Clojure.

Redshift smelled enough like PostgreSQL that we felt like we could move our
existing PostgreSQL-stored data to it and query it using the same ad-hoc tools
we had already built. Most of our data usage comes from aggregate queries, so
it seemed to perfectly fit our need. The ability to reuse both our existing code
and knowledge with PostgreSQL seemed like a no-brainer.

#### Cost

Part of the reason I like Redshift is the cost. As the co-founder of a small
startup, I have to be able to communicate effective use of our funds to
interested parties. As someone at the [Aggregate Knowledge
blog](http://blog.aggregateknowledge.com/2013/05/16/aws-redshift-how-amazon-changed-the-game/)
pointed out:

> Oddly enough, Redshift isn’t going to sell because devs think it’s
> super-duper-whizz-bang.  It’s going to sell because it took a problem
> and an industry famous for it’s opaque pricing, high TCO, and unreliable
> results and completely turned it on its head.

Amazon pricing model is quite clear:

    XL = 0.85/hr
    8XL = 8 x 0.85/hr = $6.80/hr

If you buy a reserved instance, the price goes down:

    Unreserved: $3,723 per TB per Year
    Reserved 1 year: $2,190 per TB per Year
    Reserved 3 years: $999 per TB per year

#### Speed

One of the issues we ran into is that we could not always anticipate what data
would look like prior to receiving it. We didn't want to spend an inordinate
amount of resources throwing indexes on columns that may or may not be used.
Therefore, most of our ad hoc queries were against completely unindexed data.

Since Redshift doesn't use indices, this wasn't an issue.

As a preface, any benchmark I show you is going to be somewhat arbitrary. To
properly measure this, you'd have to use an EC2 instance with properties
similar to the Redshift architecture. I didn't have time to do that, so what
I'm actually going to show you is what our "real world" speed increase looked
like.

In this example, I'm using a table that we loaded up onto a dedicated Dell
server running PostgreSQL 9.1.9.

Here's a SELECT COUNT on the table in PostgreSQL:

    # select count(*) from dummy_table;
    +----------+
    |  count   |
    +----------+
    | 21454134 |
    +----------+
    (1 row)
    Time: 586931.216 ms

That took approximately 10 minutes. And on Redshift:

    # select count(*) from dummy_table;
    count
    ----------
    21454134
    (1 row)
    Time: 1561.359 ms

1.5 seconds! That's an improvement. Note that I didn't make any adjustements to
the data: no indexes, no differences in table structure.

How about some aggregates?

    # select count(*), year, avg(total_charges) \
    from dummy_table group by year order by year desc;
    +---------+------+---------+
    |  count  | year |   avg   |
    +---------+------+---------+
    | 4926225 | 2012 | 6144.37 |
    | 8280484 | 2011 | 6149.85 |
    | 8247425 | 2010 | 5673.83 |
    +---------+------+---------+
    (3 rows)
    Time: 850491.316 ms

Approximately 15 minutes. Ouch. And Redshift:

    # select count(*), year, avg(total_charges) \
    from dummy_table group by year order by year desc;
    count  | year |   avg
    ---------+------+---------
    4926225 | 2012 | 6144.37
    8280484 | 2011 | 6149.85
    8247425 | 2010 | 5673.83
    (3 rows)
    Time: 5887.693 ms

Not bad! Definitely an improvement. There are some things we could do to make
this even faster (in both cases), but that's not really the focus here. How
much work did I have to do to prepare this data for a relatively fast aggregate
query? None at all.

### Redshift Architecture

If you log into the AWS console, the first thing you'll do is create a
*cluster.* Each cluster can have one or more Redshift databases.

A Redshift cluster consists of **leader** nodes and **compute** nodes.

A **leader** node is only created if there are two or more nodes. It is the
node that you interact with. It takes care of the planning, compiles queries
into code, and distributes it to the compute nodes. It's also where you'll find
all of the pg_ catalog tables (e.g., pg_views, pg_table_def).

If for some reason you run a SELECT query that doesn't actually touch data, it
will run on the leader node. One example of this is:

    select now()

As of August 2013, the **compute** nodes come in two flavors:
* XL: 2 Cores, 15GiB memory, 3 disk drives with 2TB of lcoal attached storage
* 8XL: 16 Cores, 120GiB memory, 24 disk drives with 16TB of lcoal attached storage
You can scale up your database by adding or removing compute nodes.

Each compute node consists of multiple slices. When you send a query to the
leader node, it compiles the query and sends it to each node. Each node
executes the query in parallel on each slice (there is one slice for each core
of the multi-core processor).

In between the leader node and all of the compute nodes is a 10GigE HPC
network. That keeps the network traffic between all of the machines snappy.

### Building Tables

Before you can load anything into Amazon Redshift, you'll have to build some
tables to store it in. This it the first thing you'll do that causes you to
notice some of the differences between Redshift and PostgreSQL.

First, Redshift "does not enforce unique, primary-key, and foreign-key
constraints." Your application code is responsible for guaranteeing uniqueness.
That being said, you will still want to add CONSTRAINT indicators to your
table. Redshift uses it to optimize its queries
([Source](http://docs.aws.amazon.com/redshift/latest/dg/c_best-practices-defining-constraints.html)).

Secondly, if you're migrating from an existing daatabase, you'll notice that
there are a lot of unsupported PostgreSQL data types. The ones that hurt the
most for us was SERIAL, since we used that for primary key columns.
Arrays, JSON, XML - all unsupported.

It's actually easier to list what *is* supported.
* SMALLINT
* INTEGER
* BIGINT
* DECIMAL
* REAL
* DOUBLE PRECISION
* BOOLEAN
* CHAR
* VARCHAR
* DATE
* TIMESTAMP

One huge gotcha in this list - if in your CREATE statement you provide a length
to VARCHAR or CHAR, note that it is byte length, not character length. This
only bites you if you store multi-byte data, but it's an important thing to
aware of when defining your data storage.  Furthermore, Redshift only
accommodates UTF8 characters up to 3 bytes long. If you're doing a lot of
internationalization, this is something you very much want to pay attention to.

-- sort key
