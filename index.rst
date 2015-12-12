.. Platformus documentation master file, created by
   sphinx-quickstart on Thu Aug 27 14:17:59 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. _index:

Introduction
============

`Platformus <https://github.com/Platformus/Platformus>`_ is free, open source and cross-platform CMS
based on ASP.NET 5 and `ExtCore framework <https://github.com/Platformus/Platformus>`_. It is built using
the best and the most modern tools and languages (Visual Studio 2015, C#, TypeScript, SCSS etc). Join our team!

Platformus is completely modular and currently consists of 8 extensions:

* Platformus.Barebone;
* Platformus.Configuration;
* Platformus.Security;
* Platformus.Static;
* Platformus.Globalization;
* Platformus.Content;
* Platformus.Navigation;
* Platformus.Forms.

Each extension may consist of several projects:

* Platformus.X;
* Platformus.X.Data.Models;
* Platformus.X.Data.Abstractions;
* Platformus.X.Data.SpecificStorageA;
* Platformus.X.Data.SpecificStorageB;
* Platformus.X.Data.SpecificStorageC;
* Platformus.X.Frontend;
* Platformus.X.Backend;
* etc.

Using the features of the underlying ExtCore framework you can easily create your own extensions
to extend the functionality of Platformus.

Contents
--------

.. toctree::
   :titlesonly:

   basic_concepts/index
   quick_start/index