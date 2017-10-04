Objects
=======

Object is the central part of the Platformus data model. It is an elementary piece of the information.
Objects are described by classes and members and consist of properties and relations. You can manage them
(add, edit, and delete) from the backend using the :guilabel:`Content/Objects` section:

.. image:: /images/fundamentals/content/objects/1.png

As we said, objects consist of properties and relationships and are described by classes and members.
Each property has its own client-side JavaScript editor, which is specified by the data type of the member.
You can create your own data types and client-side JavaScript editors. Also, data types specify
which `primitive storage data type <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Domain.Data.Entities/StorageDataType.cs#L6>`_
should be used to store the particular property value (integer, decimal, string and datetime are supported).
String properties can be localizable and nonlocalizable.

The object edit page consist of client-side JavaScript editors grouped by tabs. A typical page can look like this:

.. image:: /images/fundamentals/content/objects/2.png

The property editors may look and behave absolutely different. This is the property editor for the
``Image`` data type looks like:

.. image:: /images/fundamentals/content/objects/3.png

And this is the one for the ``Date`` data type:

.. image:: /images/fundamentals/content/objects/4.png