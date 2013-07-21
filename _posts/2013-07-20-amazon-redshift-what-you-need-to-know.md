---
layout: post
title: "Amazon Redshift: What You Need to Know"
description: "Amazon Redshift is an amazing tool, but it definitely has some quirks that can catch you unaware."
category: Programming
tags: [programming, databases, amazon, redshift, sql]
---


AVG(INT) will return an INT.
     See http://docs.aws.amazon.com/redshift/latest/dg/r_AVG.html

Using CAST for a NULL value will return a VARCHAR of unspecified length.

The s3 path you pass is a prefix. Quite handy if you want to run an EMR job and then load the output (or load from an UNLOAD command, which dumps to multiple files).

You can add only one column in each ALTER TABLE statement.
http://docs.aws.amazon.com/redshift/latest/dg/r_ALTER_TABLE.html

primary keys are not enforced. if you COPY data twice, it will happily duplicate

run ANALYZE any time you have made a non-trivial number of changes to your data

STL_LOAD_ERRORS - for error loads. use \x.

use TIMESTAMP or DATE instead of CHAR. Redshift is optimized for the former.

Sure, redshift does not enforce constraints. however, the optimizer DOES use it, so specify them anyway.

all date/timestamp columns have to be formatted in the same day (defined once in COPY) - using ACCEPTANYDATE will not generate errors but will load NULL when format does not match. [citation?]

VARCHAR(N) in postgres means a string of N characters. In redshift, it's of N bytes. doesn't matter unless you load multi-byte data.

UNLOAD to multiple files vs one file
https://forums.aws.amazon.com/message.jspa?messageID=432538

Other things:

Architecture

Leader node
- What you're talking to
- looks like postgres
- plans queries

compute notes
- executes queries in parallel via slices

10GigE HPC network between leader and compute nodes

When you're moving to Redshift, Amazon recommends spending time to test different configuration options - few large nodes vs many small notes, 16xXL versus 2x8XL

Leave your loaded files on S3 - can re-copy, easy backup
Amazon recommends UNLOAD your data to S3 or Glacial if you don't need it, you can still re-load as needed.
Deleting data is not efficient until VACUUM is run, and VACUUM is expensive, so perhaps schedule it for a less busy time.

sorting your stuff...
- want to use columns you commonly filter or group on (helps parallel execution on slices)
- if your first sort column does has low cardinality (resolution), subsequent 

Workload Manager

concurrent queries. default is 5, goes up to 15. (webinar @ 34m)
segregate short and long running queries.1111111111
set wlm_query_slot_count to 3 to increase memory for COPY or VACUUM

Choosing a sort key - how do you most commonly access the data? TIMESTAMP for "recently created"

using copy command from an s3 data bucket is "best practice"
copy multiple files at once in parallel
GZIP them if they are large
be careful about escaped data. redshift is a little finicky.
use MAXERROR and NOLOAD for debugging a new data stream
- NOLOAD speeds up file validation
- MAXERROR default is 0, remember to reset it when done
ingest via sql only as a last resort.
Amazon recommends STATUPDATE when loading significant amount of data to a non-empty table, can updates stats at the end of the load.
you need 2.5 times of your data size to load data if it's sorted, or to vacuum the table
monitor free space in performance tab, use cloudwatch alarms

debugging a load is done via the STL_LOAD_ERRORS and STL_LOADERROR_DETAIL tables.
You can check STL_LOAD_COMMITS, STL_FILE_SCAN, STL_S3CLIENT to confirm files were read.
STL_S3CLIENT_ERRR for S3 file transfer errors.

vacuum

re-sort added data based on sort keys
deleted actual data marked for deletion, re-sort table
vacuum is smart in that it avoids re-sorting slices that were unaffected
only one vacuum at a time per cluster
debugging vacuum - svv_vacuum_progress, svv_vacuum_summary



28:01 in best practices vid.

Also note that UNLOAD does dump to multiple files.

{% include JB/setup %}
