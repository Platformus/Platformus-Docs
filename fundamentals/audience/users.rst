Users
=====

Users (as well as `permissions <https://docs.platformus.net/en/latest/fundamentals/audience/permissions.html>`_
and `roles <https://docs.platformus.net/en/latest/fundamentals/audience/roles.html>`_) are used to control access
to a web application resources. You can manage them (add, edit, and delete) from the backend
using the :guilabel:`Audience/Users` section:

.. image:: /images/fundamentals/audience/users/1.png

Each user has name:

.. image:: /images/fundamentals/audience/users/2.png

Also, on the :guilabel:`Roles` tab you can assign the roles to a user:

.. image:: /images/fundamentals/audience/users/3.png

In order to be able to get to the backend, user must have the ``Administrator`` role. Please note,
that this role only allows to browse the backend, not to access any section. You can use ``Do everything`` permission
to provide access to all the sections for a role.

Let’s back to the users. While user itself has only a name, it doesn’t store any information about how it signs in.
This information is stored using the
`Credential <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Security.Data.Entities/Credential.cs#L13>`_
objects. Each user can have different credentials, and each credential has its
`type <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Security.Data.Entities/CredentialType.cs#L14>`_
(it can be email and password, Facebook account, Microsoft account and so on). When user signs in,
Platformus checks whether there is an credential with the given type, identifier, and secret exists. If the credential is found,
corresponding user is signed in.

The credential list looks like this:

.. image:: /images/fundamentals/audience/users/4.png

And this is the credential itself:

.. image:: /images/fundamentals/audience/users/5.png

(MD5 hashing algorithm will be replaced with the stronger one soon.)