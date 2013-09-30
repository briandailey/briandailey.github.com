---
layout: post
title: "Amazon Redshift - What You Need To Know"
description: ""
category: Development
tags: [amazon, redshift, sql, database]
---
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

### Why Redshift

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

One and a half seconds! That's an improvement. Note that I didn't make any adjustements to
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

**Update** As of September 2013 JSON is now supported. Thanks [@rahulpathak](https://twitter.com/rahulpathak/status/384425227934892033).

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

**Update** As [@rahulpathak](https://twitter.com/rahulpathak/status/384425227934892033) pointed
out, UTF8 up to four bytes is now supported.

#### Sort and Distribution Keys

There are two other things you want to familiarize yourself with when creating
tables on Redshift.

By default, the contents of your table are distributed across your nodes and
slices in a round-robin fashion. Evenly distributing the data means that the
slices can all share equal amounts of work. If all of the data was stored in
one slice, you couldn't take advantage of Redshift's use of parallel queries.

However, you can indicate your own *distribution key*. An ideal candidate is any
column that you commonly group by (for aggregates) or perform table joins on.
You still want to keep the data as evenly distributed as possible, however.

An example of this would be a table with an "favorite_color" column. If the
values are pretty evently distributed, then grouping them together means
Redshift has to do less work in copying data around inside the cluster to
perform the aggregate. On the other hand, if 90% of your table data has a
favorite_color of "red", then the node or slice with the "red" data is going to
have to do a disproportionate amount of work.

The *sort key* indicates how your data should be sorted on disk. You can
indicate multiple sort keys for a given table.

Here's the important thing to know:

> “Amazon Redshift stores columnar data in 1 MB disk blocks. The min and max
> values for each block are stored as part of the metadata.”

This means that if you have a sort key indicated, Redshift can skip over swaths
of your data to pinpoint exactly where the value you're looking for can be
found.

Amazon's webinars often use the example of a "last updated timestamp" column to
demonstrate how this works. If you are most commonly accessing data based on
that timestamp you can use it as a sort key. When searching for values, it will
only look at nodes, slices, and blocks that are relevant.

### ALTER

One last thing to know about building tables. If you want to ALTER a column
after the table has been created, you're [out of
luck](http://docs.aws.amazon.com/redshift/latest/dg/c_redshift-sql-implementated-differently.html).
If you want to, for example, change type or length, you'll need to ADD another
column, copy the data over, and remove the old column.

Additionally, you can only ALTER ADD COLUMN one at a time. So if you need to do
this multiple times, you're much better off creating a new table and copying
the data into it. For example:

    COPY (SELECT * FROM old_table) INTO new_table;

### Loading Data

So now that we've created out data structure, how do we get data into it? You
have two choices:

* Amazon S3
* Amazon DynamoDB

Yes, you *could* simply run a series of INSERT statements, but that is going to
be painfully slow.

Amazon recommends using the S3 method, which I will describe briefly. I don't
see the DynamoDB as particularly useful unless you're already using that and
want to migrate some of your data to Redshift.

To get the data from your local network to S3, I would use
[s3cmd](http://s3tools.org/s3cmd). It allows you to break the file into
multiple pieces for upload. Another option is to use a package like
[boto](https://github.com/boto/boto). Although it requires more work, you can
stream files concurrently rather than one at at time. As of version 1.1, s3cmd
does not allow you to load files in paralell.

    s3cmd put /path/to/my/file.sql.gz* s3://my-bucket/

There are a few things to note here. First, if you can zip your files before
uploading them, that will save you some time and bandwidth. Second, if you
break them up into multiple chunks, Redshift can load them in parallel from S3.
Note the asterisk after the file name: this assumes the file is chunked. For
example:

    file.sql.gz.0001
    file.sql.gz.0002

To get the files from S3 to Redshift, you will use the
[COPY command](http://docs.aws.amazon.com/redshift/latest/dg/r_COPY.html).

    COPY my_table (column1, column2) FROM 's3://my-bucket/file.sql.gz' WITH
    CREDENTIALS '...' GZIP

Note that the s3 path is a prefix, so it will grab all files that begin with
'file.sql.gz' and load them in parallel.

Of course, you may run into some problems at this point if your data doesn't
match the structure you're loading it into. In that case, the following tables
can be checked for details:

    STL_LOAD_ERRORS
    STL_LOADERROR_DETAIL

It is generally a good idea to run the COPY command with the NOLOAD option
first, so you can scan the entire file for any issues. It has the advantage of
running more quickly than an actual load, and you can also bump up the MAXERROR
to continue finding more problems as you scan the file. Just remember to reset
MAXERROR when you're done!

### Querying Data

The beauty of Redshift is that if you've ever used PostgreSQL, you already know
how to query it. The syntax is nearly identical. Remember to use Postgres 8.0.2
documentation, however, and always keep the [implementation
differences](http://docs.aws.amazon.com/redshift/latest/dg/c_redshift-sql-implementated-differently.html)
handy.

### Extracting Data

If you want to dump data from Redshift, you will use the
[UNLOAD](http://docs.aws.amazon.com/redshift/latest/dg/r_UNLOAD.html) command.
Note that UNLOAD will dump your query into multiple files with the prefix you
provide. This will be based on the number of slices in your cluster, so even
small queries will create multiple files. There is, however, a [way to
trick](https://forums.aws.amazon.com/message.jspa?messageID=432538)
UNLOAD into dumping everything into one file by adding an outer LIMIT.

    UNLOAD 'SELECT * FROM (
            SELECT ...
            FROM ...
            WHERE ...
        ) LIMIT 2147483647'
        ...

It does, however, affect performance.

### Optimizations

You'll want to read up on the [workload manager](http://docs.aws.amazon.com/redshift/latest/dg/c_workload_mngmt_classification.html) (WLM).
It allows you to create lanes for parallel queries, which means you can prevent long-running
queries from hogging resources.

> “By default, a cluster is configured with one queue that can run five
> queries concurrently. In addition, Amazon Redshift reserves one dedicated
> Superuser queue on the cluster, which has a concurrency level of one.
> The Superuser queue is not configurable.”

You can create up to 8 queues, and you can allow up to 15 concurrent queries.
One strategy is to set the concurrent queries to 1 when you are running a COPY
statement. That speeds up the load at the cost of making other queries wait.
You can also assign queries at runtime, or set them up by user.

When you load data, VACUUM is automatically run. However, if you make any non-trivial
changes to your data (UPDATE, DELETE, or INSERT) you will want to run it again
with ANALYZE to resort the data.

Other optimizations are highly dependent on the data you're loading. One
huge advantage of Redshift is that you can try multiple configurations (e.g.,
few large nodes vs many small notes, 16xXL versus 2x8XL) at a low cost.

### Wrap-up

The advantages of Redshift to any shop wishing to run adhoc queries against large
sets of data is abundantly clear.

* It looks and smells like PostgreSQL 8.
* It's much easier to use existing talent than learning to use a new tool like Hadoop.
  * As others have pointed out, Hadoop is generally overutilized anyway.
  * Even AirBNB analysts liked it so much they didn't want to go back to PIG and HIVE.
* It's less expensive than appliances like Vertica.
* It's pricing scheme is much more clear than competing appliances.

Making the switch from PostgreSQL to Redshift has not only made our adhoc queries faster,
it's also saved us hosting costs.

If you have any questions about our implementation, I would be happy to talk about it
further. If you're in the Nashville area, I'm always up for grabbing coffee or lunch. Feel
free to email me (brian at this domain) or ping me on Twitter at @byeliad.

This blog post is based on my notes from a talk I gave at Coderfaire 2013. Slides are
[available here](http://dailytechnology.net/talk-coderfaire-redshift-2013/).

### Additional Resources

* [AWS Webcast - Amazon Redshift Best Practices for Data Loading and Query Performance](http://www.slideshare.net/AmazonWebServices/redshift-best-practices-part-1dp2)
* [Big Data Benchmark](https://amplab.cs.berkeley.edu/benchmark/) from Berkeley, comparing Redshift, Hive, and others.
