.. _objects:

Objects
=======

Object is the central part of the default Platformus CMS data model. It is an elementary piece of the information.
It can be your blog post, comment, or tag. Objects are described by :ref:`classes <classes>` and :ref:`members <members>` and consist of properties and relations.
You can manage them (create, edit, and delete) from the backend using the :guilabel:`Content/Objects` section:

.. image:: /images/platformus_website/objects/1.png

The :guilabel:`Content/Objects` section has subsections that correspond to classes. These subsections are grouped using the parent classes.
Classes without parents go under the Other group.

As we said, objects consist of properties and relations and are described by :ref:`classes <classes>` and :ref:`members <members>`.
Each property has its own client-side editor, which is specified by the
`data type <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Data.Entities/DataType.cs#L13>`_ of the member.
As a developer, you can create your own data types and client-side editors. Also, data types specify
which `primitive storage data type <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Data.Entities/StorageDataTypes.cs#L6>`_
should be used to store the particular property value (integer, decimal, string and datetime are supported).
String properties can be localizable and non-localizable.

The object edit page consist of client-side editors grouped by :ref:`tabs <tabs>`. A typical page can look like this:

.. image:: /images/platformus_website/objects/2.png

The property editors may look and behave absolutely different. This is the property editor for the
``Image`` data type looks like:

.. image:: /images/platformus_website/objects/3.png

And this is the one for the ``Date`` data type:

.. image:: /images/platformus_website/objects/4.png