Roles
=====

Roles are used to group the permissions. For now, you can’t assign a permission to a user directly,
it is only possible to assign a role. You can manage them (add, edit, and delete) from the backend
using the :guilabel:`Audience/Roles` section:

.. image:: /images/fundamentals/audience/roles/1.png

Each role has name, code, and position. Position might be used to sort the roles in the correct order:

.. image:: /images/fundamentals/audience/roles/2.png

Also, on the :guilabel:`Permissions` tab you can assign the permissions to a role:

.. image:: /images/fundamentals/audience/roles/3.png

The same as `permissions <https://docs.platformus.net/en/latest/fundamentals/audience/permissions.html>`_,
the roles are attached to a user as the claims while signing in. You can check them from the code,
but permissions checking is preferred.