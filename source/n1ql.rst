.. _n1ql:

A N1QL for every Query
======================

.. sidebar:: Session Information

    Track 2 session by **Ilam Siva**, Senior Product Manager,
    **Couchbase**, 3:45pm, 2nd April 2014.

The real world isn't all structured and ordered.

In the traditional (relational) data model, you need to fit the data
you have into the model you've decided on. In the rich data model,
your data is varied, and your schema may vary [1]_. In the
traditional (relational) data model, data must all fit into the same
shape, and changing that shape can be costly. In the rich
(document-oriented) data model, data can fit into a multitude of
shapes, and those shapes can change easily.

SQL works well for the traditional data model, but not so well for
the rich data model, where schemas are shifting.

What is N1QL?
-------------

N1QL embraces the JSON document model, with SQL-like syntax to ease
transition. It works with structured, semi-structured, and
unstructured data. JSON is fully supported, and more formats may be
supported in future.

N1QL supports aggregations, filtering and transformations. You can,
for example, transform one array into another array. In SQL when you
run an operation, you get a result set consisting of a series of
rows. In N1QL, you operate on JSON documents, and the result of your
operation is another JSON document.

The "N1" comes from non-`first normal form
<http://en.wikipedia.org/wiki/First_normal_form>`_ - we have
multivalued attributes and nested objects.

Whilst views are fairly heavy weight, N1QL allows you to have high
performance declarative indexes which are lighter weight.

N1QL Basics
-----------

A query in N1QL has three parts to it:

* ``SELECT`` - what parts of each document do you want?
* ``FROM`` - what data bucket or data store do you want it from?
* ``WHERE`` - what conditions must be met for a document to be
  returned?

The output is in the form of a JSON document.

N1QL supports string operations such as concatenation and string
matching (including support for wildcards).

N1QL also supports ``GROUP BY``, ``ORDER BY``, as well as pagination
constructs such as ``LIMIT`` and ``OFFSET``. Other functions such as
``AVG``, ``ROUND``, ``TRUNC``, ``SUM``, ``MIN`` and ``MAX`` [2]_.

N1QL handles missing values differently from ``NULL`` values (missing
means that attribute doesn't exist in the document, ``NULL`` that it
does exist, but is ``NULL``). You can select between these two
conditions using ``IS MISSING`` and ``IS NULL``.

N1QL also allows you to join data between multiple buckets.

.. [1] Ilam said he doesn't like the term *schemaless*, since data in
       NoSQL databases still have schemas, it's just that it's
       flexible, and may vary between values.

.. [2] Ilam mentioned that a commonly asked question was whether
       user-defined functions are supported. This feature is planned,
       but not currently available.
