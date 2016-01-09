Basic Concepts
==============

With the full set of extensions Platformus is object-oriented CMS and object is the central unit
of its data model. Objects can be standalone and embedded. While standalone objects can be accessed via URL
(using some specified view), embedded objects can only be used as the part of others.

Each object consists of properties and relations and is described by its class. Classes describe properties and
relations of the objects with the members. Each member has code, name, data type (for properties) or class (for
relations). In addition, with the data sources, classes describe which objects are to be loaded together with
the object.

For example, let’s say we have Developer class and Team class. Also, we can have Contact class too. Each
developer should have first name and last name properties and one relation to the object of class Team and one
or many relations to the objects of class Contact.

.. toctree::
   :titlesonly: