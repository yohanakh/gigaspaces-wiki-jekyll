---
layout: post102
title:  Cassandra Integration
categories: XAP102
parent: big-data.html
weight: 200
---

<br>

{%section%}
{%column width=10% %}
![cassandra.png](/attachment_files/subject/cassandra.png)
{%endcolumn%}
{%column width=90% %}
The [Apache Cassandra Project™](http://cassandra.apache.org) is a scalable multi-master database with no single points of failure. The Apache Cassandra Project develops a highly scalable second-generation distributed database, bringing together Dynamo's fully distributed design and Bigtable's ColumnFamily-based data model.
{%endcolumn%}
{%endsection%}

Cassandra is in use at Digg, Facebook, Twitter, Reddit, Rackspace, Cloudkick, Cisco, SimpleGeo, Ooyala, OpenX, and more companies that have large, active data sets. The largest production cluster has over 100 TB of data in over 150 machines. Data is automatically replicated to multiple nodes for fault-tolerance. Replication across multiple data centers is supported. Failed nodes can be replaced with no downtime. Every node in the cluster is identical. There are no network bottlenecks. There are no single points of failure.

{%info%}
The current version of XAP supports `Cassandra 1.1.6`. If you need to integrate XAP with other versions of Cassandra please refer to [The Archive Container](./archive-container.html).
This will explain how to implement your own custom Archive Container.
{%endinfo%}


<br>

{%fpanel%}

[Space Persistence](./cassandra-space-persistency.html){%wbr%}
A Cassandra Space Persistency Solution

[Archive Handler](./cassandra-archive-operation-handler.html){%wbr%}
Archives space objects to a Cassandra backend.
{%endfpanel%}



