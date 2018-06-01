---
layout: post
title: "Determining AWS Redshift Spectrum Spend"
description: ""
category: programming
tags: [aws, redshift, spectrum]
---
As far as I could tell, there's no way to see a breakdown of Amazon Web Services Redshift Spectrum usage for
your most recent billing cycle. You can, however, pull this information from [`SVL_S3QUERY_SUMMARY`](https://docs.aws.amazon.com/redshift/latest/dg/r_SVL_S3QUERY_SUMMARY.html).


Assuming that the pricing is still [$5 per terabyte](https://aws.amazon.com/redshift/pricing/#redshift-spectrum-pricing) scanned, you can run this query.

```
SELECT
    SUBSTRING(querytxt, 1, 50) AS query_snippet,
    s3.starttime,
    s3.endtime,
    s3_scanned_bytes,
    (s3_scanned_bytes / (10^12) * 5) AS cost
FROM SVL_S3QUERY_SUMMARY s3 JOIN STL_QUERY q ON s3.query = q.query ORDER BY starttime DESC;
```

This will return a table like this:

```
+----------------------------------------------------+----------------------------+----------------------------+--------------------+----------------+
| query_snippet                                      | starttime                  | endtime                    | s3_scanned_bytes   | cost           |
|----------------------------------------------------+----------------------------+----------------------------+--------------------+----------------|
| select foo, bar, bat from foobarbat group by foo,  | 2018-06-01 19:32:11.362227 | 2018-06-01 19:34:43.957559 | 209502504899       | 1.0475125245   |
| select foo, bar, bat from foobarbat group by foo,  | 2018-06-01 19:08:41.76035  | 2018-06-01 19:11:13.150162 | 209502504899       | 1.0475125245   |
| select foo, bar, bat from foobarbat group by foo,  | 2018-06-01 03:26:47.284144 | 2018-06-01 03:30:17.682194 | 347280195825       | 1.73640097912  |
| select foo, bar, bat from foobarbat group by foo,  | 2018-05-31 21:34:25.677985 | 2018-05-31 21:45:59.31369  | 209502504899       | 1.0475125245   |
| select foo, bar, bat from foobarbat group by foo,  | 2018-05-31 21:27:14.332106 | 2018-05-31 21:34:25.528113 | 209502504899       | 1.0475125245   |
+----------------------------------------------------+----------------------------+----------------------------+--------------------+----------------+
```

_Was this tip useful? Leave a comment and let me know!_
