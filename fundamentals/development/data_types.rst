.. _data-types:

Data Types
==========

Data types are used to describe how the object property values should be stored, displayed, and edited in the backend.
You can manage them (add, edit, and delete) from the backend using the :guilabel:`Administration/Data Types` section:

.. image:: /images/fundamentals/development/data_types/1.png

Data Type Fields
----------------

.. image:: /images/fundamentals/development/data_types/2.png

:guilabel:`Storage data type`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is the storage-level (real) data type that is used to store the property values of this Platformus-level data type.
You can have multiple Platformus-level data types (with totally different purpose) with the same storage-level data type.
For example, ``Single line plain text`` and ``Image`` data types both use string as storage data type.

:guilabel:`JavaScript editor class name`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is the ``platformus.memberEditors`` JavaScript object’s property name. Another JavaScript object is assigned to this property.
This object is used to build the client-side editors for the Platformus-level object’s properties of this data type.
For example, please take a look at the `singleLinePlainText <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Domain.Backend/Areas/Backend/Scripts/MemberEditors/single_line_plain_text_member_editor.js#L6>`_ editor.

When the object page is going to be displayed in the backend, editors for all the object properties are created.
Each editor is created using `such JavaScript object <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Domain.Backend/Areas/Backend/Scripts/MemberEditors/member_editors.js#L25-L27>`_.

You can easily write your own JavaScript client-side editors and then use them in the standard or custom data types.

:guilabel:`Name`
~~~~~~~~~~~~~~~~

Name is used to identify the data types in the backend.

:guilabel:`Position`
~~~~~~~~~~~~~~~~~~~~

Position is used to sort the data types in the lists.