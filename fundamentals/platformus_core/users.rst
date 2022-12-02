.. _users:

Users
=====

Users (as well as :ref:`permissions <permissions>` and :ref:`roles <roles>`)
are used to control access to a web application resources.
You can manage them (create, edit, and delete) from the backend using the :guilabel:`Audience/Users` section:

.. image:: /images/fundamentals/audience/users/1.png

Each user has name:

.. image:: /images/fundamentals/audience/users/2.png

Also, on the :guilabel:`Roles` tab you can assign the roles to a user:

.. image:: /images/fundamentals/audience/users/3.png

While user itself has only a name, it doesn’t store any information about how it signs in.
This information is stored using the
`Credential <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Data.Entities/Credential.cs#L13>`_
objects. Each user can have different credentials, and each credential has its
`type <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Data.Entities/CredentialType.cs#L14>`_
(it can be email and password, Facebook account, Microsoft account and so on). When user signs in,
Platformus checks whether there is a credential with the given type, identifier, and secret exists. If the credential is found,
corresponding user is signed in.

The credential list looks like this:

.. image:: /images/fundamentals/audience/users/4.png

And this is the credential itself:

.. image:: /images/fundamentals/audience/users/5.png