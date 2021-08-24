Configurations
==============

Configurations and variables are used to provide user-defined configuration parameters to the web application
(while developer-defined ones can be provided using the appsettings.json file).
You can manage them (crate, edit, and delete) from the backend using the :guilabel:`Administration/Configurations` section:

.. image:: /images/fundamentals/administration/configurations/1.png

Each configuration has code and name:

.. image:: /images/fundamentals/administration/configurations/2.png

Code is used to get the configuration from code.

Configurations consist of variables. Each variable has code, name, value, and position:

.. image:: /images/fundamentals/administration/configurations/3.png

The same as for configurations, code is used to get the variable from code.

There is the special
`DefaultConfigurationManager <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core/Services/Defaults/DefaultConfigurationManager.cs#L12>`_
class that you can use to access the configurations. It implements the
`IConfigurationManager <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core/Services/Abstractions/IConfigurationManager.cs#L6>`_
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