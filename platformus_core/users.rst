.. _users:

Users
=====

Users (as well as :ref:`permissions <permissions>` and :ref:`roles <roles>`)
are used to control access to a web application resources.
You can manage them (create, edit, and delete) from the backend using the :guilabel:`Audience/Users` section:

.. image:: /images/platformus_core/users/1.png

Each user has name:

.. image:: /images/platformus_core/users/2.png

Also, on the :guilabel:`Roles` tab you can assign the roles to a user:

.. image:: /images/platformus_core/users/3.png

As user itself only has a name, he doesn’t store any information about how he signs in.
This information is stored using the
`Credential <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Data.Entities/Credential.cs#L13>`_
objects. Each user can have different credentials, and each credential has its
`type <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Data.Entities/CredentialType.cs#L14>`_
(it can be email and password, Facebook account, Microsoft account and so on). When user signs in,
Platformus checks if there is a credential with the given type, identifier, and secret exists. If the credential is found,
corresponding user is signed in.

The credential list looks like this:

.. image:: /images/platformus_core/users/4.png

Each credential has type, identifier, and secret:

.. image:: /images/platformus_core/users/5.png

:guilabel:`Credential type`
~~~~~~~~~~~~~~~~~~~~~~~~~~~

As a developer, you can create your own credential types which depend on the sign in methods your application supports.

:guilabel:`Secret`
~~~~~~~~~~~~~~~~~~

``Secret`` is optional and can be used to store any additional information. For example, it stores passwords (as hashes)
for the email and password credential type. If you need to change the password, just type it into this field.
Don’t forget to set the :guilabel:`Apply PBKDF2 hashing to secret` checkbox to apply hashing,
otherwise your password will be saved as plain text and signing in won’t work (as it compares hashes).