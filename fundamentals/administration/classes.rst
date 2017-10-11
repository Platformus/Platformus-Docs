Classes
=======

Classes are used to describe the objects. Using the members, they describe which properties should the objects have,
how these property values should be stored and edited in the backend. You can manage them (add, edit, and delete)
from the backend using the :guilabel:`Administration/Classes` section:

.. image:: /images/fundamentals/administration/classes/1.png

Data Type Fields
----------------

.. image:: /images/fundamentals/administration/classes/2.png

:guilabel:`Parent class (abstract only)`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you select a parent class, your class will have all the tabs and members of that abstract class.
This feature helps to avoid copying the same members again and again. For example, it is good idea to have the ``Page`` class
with such members, like ``URL``, ``Content``, ``Title``, and ``META`` tags.
Also, abstract classes are used to group the objects in the :guilabel:`Content/Objects` section.

:guilabel:`Code`
~~~~~~~~~~~~~~~~

It is the unique text identifier of the class. For example, it is used in the Platformus API to specify,
which class of objects you want to manipulate.

:guilabel:`Name`
~~~~~~~~~~~~~~~~

Name is used to identify the classes in the backend.

:guilabel:`Pluralized name`
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pluralized name is used to as the object list titles.

:guilabel:`Is abstract`
~~~~~~~~~~~~~~~~~~~~~~~

Specifies whether the class is abstract or not (see above).

Tabs
----

Tabs are used to group the object property editors on the object page. Click the :guilabel:`Tabs` link in the class row:

.. image:: /images/fundamentals/administration/classes/3.png

Tab Fields
----------

.. image:: /images/fundamentals/administration/classes/4.png

:guilabel:`Name`
~~~~~~~~~~~~~~~~

Name is used to identify the tabs in the backend.

:guilabel:`Position`
~~~~~~~~~~~~~~~~~~~~

Position is used to sort the tabs in the lists.

Members
-------

Members are used to describe which properties should have the objects of a given class. Click the :guilabel:`Members` link
in the class row:

.. image:: /images/fundamentals/administration/classes/5.png

Member Fields
-------------

.. image:: /images/fundamentals/administration/classes/6.png

:guilabel:`General/Tab`
~~~~~~~~~~~~~~~~~~~~~~~

You can select a tab this member should belong to. All the members without a tab selected go under the :guilabel:`General` tab.

:guilabel:`General/Code`
~~~~~~~~~~~~~~~~~~~~~~~~

It is the unique text identifier of the member. This code is used in the different places, like sorting, mapping etc.

:guilabel:`General/Name`
~~~~~~~~~~~~~~~~~~~~~~~~

Name is used to identify the members in the backend.

:guilabel:`General/Position`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Position is used to sort the members in the lists.

.. image:: /images/fundamentals/administration/classes/7.png

:guilabel:`Property/Property data type`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Member can be a property or a relation. If you specify the property data type, member will be considered as a property.
Property data type allows to specify how to store the object property value (and which raw storage data type is used for that),
how to display and edit it in the backend.

If a property data type is selected, data type parameters will be also displayed.

.. image:: /images/fundamentals/administration/classes/8.png

:guilabel:`Relation/Relation class`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you specify the relation class, member will be considered as a relation. Relation selector will be displayed as the editor.
Also, if any relation class is selected, additional fields will be displayed.

:guilabel:`Is relation single parent`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Specifies whether objects of this class can have the only one relation to the specified class (and this specified class will be considered
as the parent one for the current class). For example, if blog post page can have the only one category page, you can use this option.
In the object list link to the blog post pages will appear in the category page rows, so all the created blog post pages will be automatically related
to the parent category page objects. If the checkbox is not set, there will be two separated lists of the objects: ``Category pages`` and ``Blog post pages``,
and you will have to select a category page in every blog post page from the relation selector manually.

:guilabel:`Relation/Min related objects number` and :guilabel:`Relation/Max related objects number`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These fields allow to limit the number of the related objects. For example, you can specify that there should be 3-5 tags on every blog post page,
so user will not be able to create a blog post page without the tags, or to specify more than 5.