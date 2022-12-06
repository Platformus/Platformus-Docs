Fundamentals
============

Platformus CMS is modular and extendable, so its behavior is very dependent on the set of the extensions.
The main and the only required extension is the Platformus.Core. It doesn’t provide any content management,
instead it implements such basic things like reusable admin panel (or backend) UI, user access control,
configuration, localization etc.

Depending on your needs and requirements you can either use other existing extensions to manage your content
or write your own one(s). Anyway, the main purpose of the Platformus CMS is to save you from writing routine code,
to speed up development, and to provide you with convenient and standardized admin panel UI. Also,
you can write and then reuse small typical extensions from project to project.

Standard Extensions
-------------------

.. toctree::
   :titlesonly:

   platformus_core/index
   platformus_website/index
   platformus_ecommerce/index
   platformus_images/index

There are several use cases as examples.

Mobile app API and admin panel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can create an empty web application, add dependencies on the Platformus.Core extension packages,
and write a custom extension that will contain all the application-specific things:  entities, models, DTOs,
controllers, admin panel sections etc.

In this case you have the very basic things out of the box and do not need to think about backend UI,
combining it using the built-in tag helpers like bricks. At the same time, CMS has no effect on performance,
so you can get maximum of what the .NET gives.

Website
~~~~~~~

Most of the websites’ content is changed from time to time, so if you are using a cache,
it could be not so important how many milliseconds it takes to retrieve from a database and display your data.
Development speed is much more important in such cases.

In such cases you can use Platformus.Website extension. It provides features to describe your content with classes
and then create and use it as objects. This extension allows to avoid programming and, in many cases, trivial configuration
and writing Razor views could be enough.

Ecommerce
~~~~~~~~~

Platformus CMS contains Platformus.Ecommerce extension which (as any other) can be used as the NuGet packages,
or as the source code. The second option could be useful when you need a very specific ecommerce app,
so you can just use the source code as a simple barebone and implement features you need.

All these approaches do not exclude each other and can be combined.