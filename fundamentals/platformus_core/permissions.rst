.. _permissions:

Permissions
===========

Permissions are used to control user access to a web application resources. You can manage them (create, edit, and delete)
from the backend using the :guilabel:`Audience/Permissions` section:

.. image:: /images/fundamentals/audience/permissions/1.png

Each permission has name, code, and position. Code is used to check permission from code, while position might be used to sort the permissions in the correct order:

.. image:: /images/fundamentals/audience/permissions/2.png

Once you created a permission, you can assign it to a :ref:`role <roles>` (and then to a :ref:`user <users>`).
While signing in, all the user roles and all the permissions from that roles are attached to the user as the claims.
These claims then can be checked from the code:

.. code-block:: cs
    :emphasize-lines: 1

    if (context.User.HasClaim(PlatformusClaimTypes.Permission, Permissions.ManageUsers))
    {
    }

Platformus uses authorization policies to control access to the controllers and actions:

.. code-block:: cs
    :emphasize-lines: 2

    [Area("Backend")]
    [Authorize(Policy = Policies.HasManageUsersPermission)]
    public class UsersController : ControllerBase { }

In order to be able to use an authorization policy, it should be
`added to the authorization options <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core/Actions/AddAuthorizationAction.cs#L20>`_
inside the ``services.AddAuthorization()`` extension method:

.. code-block:: cs
    :emphasize-lines: 4

    services.AddAuthorization(options =>
      {
        foreach (IAuthorizationPolicyProvider authorizationPolicyProvider in ExtensionManager.GetInstances<IAuthorizationPolicyProvider>())
          options.AddPolicy(authorizationPolicyProvider.Name, authorizationPolicyProvider.GetAuthorizationPolicy());
        }
      );

As you can see, the ExtCore framework’s
`ExtensionManager <https://github.com/ExtCore/ExtCore/blob/master/src/ExtCore.Infrastructure/ExtensionManager.cs#L16>`_
class is used to get all the instances of the
`IAuthorizationPolicyProvider <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core/IAuthorizationPolicyProvider.cs#L14>`_
interface implementations. Then method ``IAuthorizationPolicyProvider.GetAuthorizationPolicy()`` is used
to get the authorization policies.

So, if the permission is used to control access to a controller or action via policy, you need to implement
the ``IAuthorizationPolicyProvider`` interface and then add corresponding attribute to the controller or action.
If you only want to check the permission from code,  you don’t have to implement that interface.