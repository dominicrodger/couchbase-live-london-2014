.. _amadeus:

Opening Keynote: Amadeus Case Study
===================================

*Session by Dietmar Fauser, VP, Architecture, Quality & Governance,
Amadeus.*

Amadeus sits between travel providers and travels agents, linking up
travel agents with hotels, flights, etc. The main users of their
systems are travel agents (both traditional agencies such as Thomson
and online agencies like Expedia).

They also work on tools for airlines and hotels for managing
inventory. 800 million passengers will travel with flights arranged
by Amadeus in 2015.

Handle up to 24,000 operations per second, with a 0.5 second response
time, dealing in petabytes of data.

Were previously using Oracle in a non-relational manner (serialised
blobs of data). Prototyped 2 projects in Couchbase in 2013.

Determining Flight Availability
-------------------------------

Given a particular flight, date and the point of sale, they need to
be able to determine availability (point of sale is relevant because
of currency exchange rates - you might want to prioritise different
regions depending on current exhcange rates).

When communicating with external airline inventories, queries are
traditionally cached. This leads to problems:

1. Non-competitive prices (fresher data might give cheaper seats);
2. Rejecting bookings which could actually be fulfilled.

Customers can shift transactions to other brokers if results from
Amadeus aren't as good as a competitor's results. Stale caches
therefore cost money.

Prior to Couchbase, they had a memcached layer sitting on top of a
MySQL farm sitting on top of Oracle. Scaling any of these layers was
a major undertaking. The application layer currently has to know
about the server topology, which makes scaling it or changing it
impractical. memcached outages are very disruptive, since all load
then goes to MySQL, which can't handle it.

With Couchbase, they lose the MySQL and memcached layers, and just
have 30 Couchbase servers, with 1TB of RAM each.

During node failover, they read from replicas (for their case,
reading dirty data is better than no data) - this was a feature they
requested, that came in Couchbase 2.1.0.

They operate a single data centre, with 6 different isolated zones -
they can lose one zone without losing data.

They're using Couchbase for a distributed session store, sharing
users' session information across the tier of apllication servers.

Features they're after
----------------------

* Partial bucket replication;
* A better security model;
* The ability to audit transactions.
