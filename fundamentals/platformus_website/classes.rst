.. _classes:

Classes
=======

Classes are used to describe the :ref:`objects <objects>`. Using the :ref:`members <members>`, they describe which properties should the objects have,
how these property values should be stored and edited in the backend, and how the objects are related to each other.
You can manage them (create, edit, and delete) from the backend using the :guilabel:`Development/Classes` section:

.. image:: /images/fundamentals/development/classes/1.png

Each class has optional parent class, code, name, and other fields:

.. image:: /images/fundamentals/development/classes/2.png

:guilabel:`Parent class (abstract only)`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you select a parent class, your class will have all the tabs and members of that abstract class.
This feature helps to avoid copying the same members again and again. For example, it is good idea to have the ``Page`` abstract class
with such members, like ``URL``, ``Content``, ``Title``, and ``META`` tags.
Also, abstract classes are used to group the objects in the :guilabel:`Content/Objects` section.

:guilabel:`Code`
~~~~~~~~~~~~~~~~

It is the unique text identifier of the class.

:guilabel:`Name`
~~~~~~~~~~~~~~~~

Name is used to identify the classes in the backend.

:guilabel:`Pluralized name`
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pluralized name is used in the :guilabel:`Content/Objects` section.

:guilabel:`Is abstract`
~~~~~~~~~~~~~~~~~~~~~~~

Specifies whether the class is abstract or not.