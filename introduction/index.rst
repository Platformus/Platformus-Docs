﻿Introduction
============

`Platformus <https://github.com/Platformus/Platformus>`_ is free, open source and cross-platform CMS
based on ASP.NET Core and `ExtCore framework <https://github.com/ExtCore/ExtCore>`_. It is built using
the best and the most modern tools and languages (Visual Studio 2015, C#, TypeScript, SCSS etc). Join our team!

Few Facts About Platformus
--------------------------

1. It runs on Windows, Mac and Linux.
2. It is completely modular and extendable. Using the features of the underlying
   `ExtCore framework <https://github.com/ExtCore/ExtCore>`_ you can easily create your own extensions
   to extend its functionality.
3. It is multicultural and multilingual.
4. It is fast, flexible and easy to use. You can describe even complicated entities and their relationships
   without writing any code!

Basic Concepts
--------------

With the full set of the extensions Platformus is object-oriented CMS and object is the central unit of its
data model. Objects can be standalone and embedded. While standalone object can be accessed via URL (using
some specified view), embedded object can only be used as the part of others.

Each object consists of properties and relations and is described by its class. Classes describe properties and
relations of the objects with the members. Each member has code, name, data type (for properties) or class (for
relations). In addition, with the data sources, classes describe which objects are to be loaded together with
the object.

For example, let’s say we have Developer class and Team class. Also, we can have Contact class too. Each
developer should have first name and last name properties and one relation to the object of class Team and one
or many relations to the objects of class Contact.