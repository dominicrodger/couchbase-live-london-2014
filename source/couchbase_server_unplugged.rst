Couchbase Server Unplugged
==========================

*Session by Ravi Mayuram, VP of Engineering, Couchbase.*

Why do we need Couchbase Server?
--------------------------------

.. epigraph::

    Tape is dead, disk is tape, flash is disk, RAM locality is King.

    -- Jim Gray (2006)

As memory gets cheaper and cheaper, keeping data in RAM becomes a
more attractive and practical proposition.

Increasingly data is represented as JSON at application boundaries.

What is Couchbase Server?
-------------------------

Couchbase Server allows for **Layer Consolidation** - one layer
subsumes another, both layers benefit and share common services (as
demonstrated in the keynotes from :ref:`Viber <viber>` and
:ref:`Amadeus <amadeus>`) having fewer layers reduces the logic
needed to keep them in sync.

Couchbase is a distributed, master-less, shared-nothing,
memory-first, auto-sharded document databases that is built to
perform at web-scale.

Couchbase is a document-database paired with a cache (i.e. we keep
stuff in memory).

N1QL
----

N1QL (/ˈnɪkəl/) is an expressive, SQL-like query languages. The "N1"
comes from non-`first normal form
<http://en.wikipedia.org/wiki/First_normal_form>`_, meaning we relax
the requirements of first normal form, allowing for duplication of
data. See my notes on the :ref:`N1QL <n1ql>` session.

Common use cases
----------------

* Social gaming
* Ad targeting
* User profile store
* Session store
* Content and metadata store
* High availability cache
