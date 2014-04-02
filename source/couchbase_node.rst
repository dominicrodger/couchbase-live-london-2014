Node.js & Couchbase - Full Stack JSON
=====================================

*Session by Philipp Fehre, Technical Evangelist, Couchbase.*

To make a game API, you need to make things fast, and you need to be
able to scale. Most players won't pay you anything, so you need to be
resource-efficient too, so that you can still make money.

node.js has an event-driven programming model. Most node.js apps have
little state, and can be scaled by adding application servers (with
appropriate load balancing). You then need a data store that can be
talked to by multiple application servers.

Couchbase recognises JSON as a datatype, allowing us to do more
complex queries on JSON values using views and map/reduce.


.. note::

   Much of this session was demonstrating code, so there aren't a lot
   of notes.
