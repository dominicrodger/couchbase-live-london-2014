Anatomy of a Couchbase App
==========================

.. sidebar:: Session Information

    Track 2 session by **Matthew Revell & J Chris Anderson**,
    **Couchbase**, 11:05am, 2nd April 2014.

J Chris Anderson demonstrated a web app somewhat similar to Snapchat, which:

* uses Couchbase for asset storage and keyspace management;
* doesn't require complex queries - build your Couchbase key using
  predictable key patterns;
* uses Couchbase to provide ordering, immutable keys and expiry;
* is built with Express, React.js and PubNub.

How it works
------------

* The app asks the server for a message ID;
* The server hands them out sequentially and atomically;
* The app saves images and audio to URLs based on the message ID;
* Optionally allow messages to self-destruct.

The latency sensitive path just uses key-value operations (getting
documents that are referred to by other documents can be done in a
reasonable timeframe using two round-trips). The messages in a room
are just the messages from 0 to the current message number, so the
app just does a bunch of sequential gets.

Scaling
-------

Since there's not a lot of logic on the application server (it's
effectively stateless), we can scale by adding machines and balancing
load between machines.
