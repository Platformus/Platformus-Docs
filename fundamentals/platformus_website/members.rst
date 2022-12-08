.. _members:

Members
=======

Members are used to describe which properties and relations should the objects of a given class have.
You can manage them (create, edit, and delete) from the backend using the :guilabel:`Members` section of the :ref:`classes <classes>`:

.. image:: /images/fundamentals/development/members/1.png

Each member has tab, code, name, and other fields:

.. image:: /images/fundamentals/development/members/2.png

:guilabel:`General/Tab`
~~~~~~~~~~~~~~~~~~~~~~~

You can select a tab this member properties should belong to. All the properties of the members without a tab selected go under the :guilabel:`General` one.

:guilabel:`General/Code`
~~~~~~~~~~~~~~~~~~~~~~~~

It is the unique text identifier of the member. This code is used in the different places, like sorting, mapping etc.

:guilabel:`General/Name`
~~~~~~~~~~~~~~~~~~~~~~~~

Name is used to identify the members in the backend.

:guilabel:`General/Position`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Position is used to sort the members in the lists.

.. image:: /images/fundamentals/development/members/3.png

:guilabel:`Property/Property data type`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Member can be a property or a relation. If you specify the property data type, member will be considered as a property.
Property data type allows to specify how to store the object property value (and which
`raw storage data type <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Data.Entities/StorageDataTypes.cs#L6>`_
is used for that), how to display and edit it in the backend.

If a property data type is selected, data type parameters will be also displayed. Each data type can have unique parameters.
For example, it could be maximum text length for the text or width and height for the image.

.. image:: /images/fundamentals/development/members/4.png

:guilabel:`Relation/Relation class`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you specify the relation :ref:`class <classes>`, member will be considered as a relation. Relation selector will be displayed as the editor.
For example, user will be able to select a category for a blog post or assign tags to it. Also, if any relation class is selected,
additional fields will be displayed.

:guilabel:`Is relation single parent`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Specifies whether objects of this class can have the only one relation to the specified class (and this specified class will be considered
as the parent one for the current class). For example, if blog post page can have the only one category page, you can use this option.
In the object list, link to the blog post pages will appear in the category page rows, so all the created blog post pages will be automatically related
to the parent category page objects. If the checkbox is not set, there will be two separated lists of the objects: ``Category pages`` and ``Post pages``,
and you will have to select a category page in every post page from the relation selector manually.

:guilabel:`Relation/Min related objects number` and :guilabel:`Relation/Max related objects number`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These fields allow to limit the number of the related objects. For example, you can specify that there should be 3-5 tags on every blog post page,
so user will not be able to create a blog post page without the tags, or to specify more than 5.