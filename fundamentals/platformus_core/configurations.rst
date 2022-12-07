.. _configurations:

Configurations
==============

Configurations and variables are used to provide user-defined configuration parameters to the web application
(while developer-defined ones can be provided using the appsettings.json file).
You can manage them (create, edit, and delete) from the backend using the :guilabel:`Administration/Configurations` section:

.. image:: /images/fundamentals/administration/configurations/1.png

Each configuration has code and name:

.. image:: /images/fundamentals/administration/configurations/2.png

:guilabel:`Code`
~~~~~~~~~~~~~~~~

``Code`` might be used to get configuration from code (see examples below).

Configurations consist of variables. Each variable has code, name, value, and position:

.. image:: /images/fundamentals/administration/configurations/3.png

:guilabel:`Code`
~~~~~~~~~~~~~~~~

The same as for configurations, ``Code`` is used to get variable from code.

:guilabel:`Value`
~~~~~~~~~~~~~~~~~~~~

``Value`` contains the variable's value.

:guilabel:`Position`
~~~~~~~~~~~~~~~~~~~~

``Position`` might be used to sort the variables in the correct order.

There is the special
`DefaultConfigurationManager <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core/Services/Defaults/DefaultConfigurationManager.cs#L12>`_
class that you can use to access the configurations. It implements the
`IConfigurationManager <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core/Services/Abstractions/IConfigurationManager.cs#L9>`_
interface and it is registered as a service inside the DI, so you can replace it with your own implementation.

This is the usage example:

.. code-block:: cs
    :emphasize-lines: 5

    public class DefaultController : Controller
    {
      public DefaultController(IConfigurationManager configurationManager)
      {
        string emailSmtpServer = configurationManager["Email", "SmtpServer"];
      }
    }

This will get value of the variable with code ``SmtpServer`` from the configuration with code ``Email``.