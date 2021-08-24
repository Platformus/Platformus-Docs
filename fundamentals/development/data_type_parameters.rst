.. _data-type-parameters:

Data Type Parameters
====================

Each data type can have parameters. For example, the ``Single line plain text`` data type has the
``Is required`` and ``Max length`` parameters:

.. image:: /images/fundamentals/development/data_type_parameters/1.png

When developer creates a class member with the given data type, he can specify values for these parameters.
Later when the JavaScript object property editors are being created, these values can be accessed and used.

Each data type parameter has JavaScript editor class name, code, and name:

.. image:: /images/fundamentals/development/data_type_parameters/2.png

:guilabel:`JavaScript editor class name`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Data type parameters can have `different type <https://github.com/Platformus/Platformus/tree/master/src/Platformus.Core.Backend/Areas/Backend/Scripts/ParameterEditors>`_.
For example, ``textBox`` or ``checkbox``. It determines how user edits the parameter's value.

:guilabel:`Code`
~~~~~~~~~~~~~~~~

Code is used to get the parameter's value from the JavaScript property editor.

:guilabel:`Name`
~~~~~~~~~~~~~~~~

Name is used only in the data type parameter list to identify data type parameters.