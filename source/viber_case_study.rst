.. _viber:

Opening Keynote: Viber Case Study
=================================

.. sidebar:: Session Information

    Keynote session by **Amir Ish-Shalom**, System Architect,
    **Viber**, 10:15pm, 2nd April 2014.

Viber originated three years ago as an iPhone app for VOIP, they've
now got text messaging, video chat, and a version for
Android. Starting to make money by allowing calls to landlines and
mobiles, and selling sticker packages.

They have over 300 million users, growing at 1 million a
day. Billions of messages are send every month, and billions of
minutes of voice.

Original Architecture
---------------------

Viber originated with a tier of application servers, backed by an
in-house, in-memory database.

In 2011, they used MongoDB, including a very early version of
MongoDB's sharding support. They then added a Redis cache (purely in
memory) in front of MongoDB. Eventually, they had performance
problems with MongoDB, so they became more and more reliant on
Redis. Redis had no support for sharding, so they wrote their own
frontend which dealt with sharding. MongoDB continued to be a problem
for performance, so they moved some data to be solely in Redis (circa
2013).

Things that went well:

* It got them through an abrupt growth path;
* They never lost data in MongoDB;
* Redis has reliably good performance.

Things that went badly:

* MongoDB could only managed tens of thousands of operations per
  second, they needed hundreds of thousands. Large datasets cause
  MongoDB problems.
* MongoDB does not scale well with many application servers (it
  handles each connection in a separate thread, which ends up being
  very wasteful of CPU and memory).
* The inhouse sharding frontend for Redis wasn't easily scalable (it
  could only handle increasing the number of servers by factors of
  two).

They ended up with:

* 1 MongoDB cluster with 150 servers (master and two slaves)
* 3 Redis clusters with a total of around 150 servers.

Current Architecture
--------------------

Needs:

* Very high performance - up to a million operations per second;
* Handling very large data sets;
* Elasticity without performance disruption;
* Using AWS, so node failures are common - they need a system that
  can handle node failures without service disruption;
* Backup handling;
* High availability;
* Good monitoring capabilities;
* They'd prefer a single database - providing both a caching layer
  and a persistence layer.

They've opted for small nodes (about 60GB RAM per node). They have
separate nodes for different types of operations (reads vs sets vs
appends). They have at most 60 nodes per cluster. They use XDCR to
backup to a backup cluster. All views are done on their backup
clusters, not on production clusters. Backups are then sent to disk,
and sent to S3.

They currently have over 400 application servers, along with:

* 7 Couchbase clusters, each with up to 60 nodes;
* 0-2 replicas, XDCR and external backups;
* They have a total of 150 Couchbase servers (less than half the
  number needed with MongoDB and Redis).

Their busy read clusters are handling hundreds of thousands of reads
per second, on 10 node clusters.

Migration to Couchbase
----------------------

Migration was done live, with no downtime, and with no data loss, and
with data remaining consistent.

5 clusters are migrated, 1 is in progress, and 1 remains to be
done. MongoDB is now retired, so there's just 2 Redis clusters
remaining.

They're interested in Couchbase 2.5 for rack awareness of replicas
(since they're using AWS, they need to make sure their replicas
aren't in the same availability zones as the active copies).

They're looking to use Elastic Search using XDCR for full text
search.
