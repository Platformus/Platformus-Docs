.. _roles:

Roles
=====

Roles are used to group the permissions. You can’t assign a permission to a user directly,
it is only possible to assign a role. You can manage them (create, edit, and delete) from the backend
using the :guilabel:`Audience/Roles` section:

.. image:: /images/platformus_core/roles/1.png

Each role has name, code, position, and other fields:

.. image:: /images/platformus_core/roles/2.png

:guilabel:`General/Code`
~~~~~~~~~~~~~~~~~~~~~~~~

``Code`` might be used to check roles from code.

:guilabel:`General/Position`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``Position`` might be used to sort the roles in the correct order.

Also, on the :guilabel:`Permissions` tab you can assign the permissions to a role:

.. image:: /images/platformus_core/roles/3.png

The same as :ref:`permissions <permissions>`, roles are attached to a user as the claims while signing in.
You can check them from the code to control rights and restrict access, but permissions checking is preferred.