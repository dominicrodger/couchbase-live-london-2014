The Art & Science of Document Modelling
=======================================

.. sidebar:: Session Information

    Track 2 session by **Jasdeep Jaitla**, Technical Evangelist,
    **Couchbase**, 11:50am, 2nd April 2014.

Basics of Data in Couchbase
---------------------------

There are three types of keys in Couchbase:

1. Deterministic - human readable;
2. Random - e.g. UUID;
3. Pseudo-random - e.g. user-<UUID> - human-readable random keys, but
   with the ability to figure out what sort of document it's going to
   be based on the key.

There are three types of data in Couchbase:

1. Primitive data types (e.g. ``98.6`` or ``true``);
2. JSON;
3. Binary.

Each key-value pair has two components - metadata and the
document. The metadata contains the key, the revision, some flags,
expiration information, and type information. The metadata is 56
bytes, plus however many bytes the key is. Metadata is kept in RAM,
to allow very quick responses in error conditions (e.g. calling
``add`` on a key that already exists).

Keys are partitioned into vBuckets by taking a ``crc32`` hash of the
key, and picking an appropriate vBucket. vBuckets are distributed
across clusters, and rebalancing is the process of moving
vBuckets. ``crc32`` evenly distributes keys across vBuckets, and
vBuckets are distributed evenly across servers.

Key Selection
-------------

Deterministic keys make fetching data very straightforward. For
example - if users log in using email address, the email address
makes a good key. However - what if users can also log in with a
username? We can work around that by adding a lookup-key - if the
username is ``dominic``, and the email is ``dominic@example.com``, we
add two documents at sign up:

1. ``dominic`` with the value ``dominic@example.com``;
2. ``dominic@example.com``, which contains the account information.

Since read operations are fairly quick, we can just use two
round-trips.

An alternative to this approach is looking up usernames with a view,
which gives you the user record directly from the username. This will
involve asking each node in the Couchbase cluster (since each node
has the subset of the view for the records which are active on that
node).
