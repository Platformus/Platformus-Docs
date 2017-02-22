Tutorial: Create Simple Platformus-Based Web Application
========================================================

We are going to create simple Platformus-based web application. First of all,
if you are new to ASP.NET Core please visit `this page <https://www.microsoft.com/net/core>`_. You
will find there everything you need to start developing ASP.NET Core web applications.

Platformus consists of the set of `ExtCore <http://extcore.net/>`_ extensions (NuGet packages) and
can’t be run directly. To run it we need to have host (or main) web application that contains all
user content like views, images, css, js etc. When the new version of Platformus is released we
can easily update it without losing any data. So we have two options here:

1. Download ready to use `Platformus-Prod <http://platformus.net/en/download>`_. It is compiled
and published Platformus-Based web application that contains everything you need to start creating
your web application (even without any programming skills), including SQLite database and some
default basic content. It can be run locally or on a web server and configured using the backend.
You still can use custom or third-party extensions but if you want to have more control over the
process consider using the next option.

2. Create your own host web application. In this case you will have to manually add dependencies
on Platformus packages, write some code and create configuration file, database etc.

Download Ready to Use Platformus-Prod
-------------------------------------

After Platformus-Prod archive is downloaded and extracted run the following commands in the
console:

.. code-block:: bat

    cd [path to the extracted archive]
    dotnet webapplication.dll

You should have the following result:

.. image:: /images/tutorial_simple/1.png

Now open your browser and navigate to http://localhost:5000/:

.. image:: /images/tutorial_simple/2.png

Your Platformus-based web application is ready to use.

Create Your Own Host Web Application
------------------------------------

Let’s start Visual Studio and create new ASP.NET Core project:

.. image:: /images/tutorial_simple/3.png

.. image:: /images/tutorial_simple/4.png

Empty project is created.

Open project.json file and add dependencies on the following packages:

* Platformus.Configurations, version 1.0.0-alpha14;
* Platformus.Configurations.Backend, version 1.0.0-alpha14;
* Platformus.Configurations.Data.EntityFramework.Sqlite, version 1.0.0-alpha14;
* Platformus.Domain.Api, version 1.0.0-alpha14;
* Platformus.Domain.Backend, version 1.0.0-alpha14;
* Platformus.Domain.Data.EntityFramework.Sqlite, version 1.0.0-alpha14;
* Platformus.Domain.Frontend, version 1.0.0-alpha14;
* Platformus.FileManager.Backend, version 1.0.0-alpha14;
* Platformus.FileManager.Data.EntityFramework.Sqlite, version 1.0.0-alpha14;
* Platformus.Forms.Backend, version 1.0.0-alpha14;
* Platformus.Forms.Data.EntityFramework.Sqlite, version 1.0.0-alpha14;
* Platformus.Forms.Frontend, version 1.0.0-alpha14;
* Platformus.Globalization.Backend, version 1.0.0-alpha14;
* Platformus.Globalization.Data.EntityFramework.Sqlite, version 1.0.0-alpha14;
* Platformus.Globalization.Frontend, version 1.0.0-alpha14;
* Platformus.Menus.Backend, version 1.0.0-alpha14;
* Platformus.Menus.Data.EntityFramework.Sqlite, version 1.0.0-alpha14;
* Platformus.Menus.Frontend, version 1.0.0-alpha14;
* Platformus.Security.Backend, version 1.0.0-alpha14;
* Platformus.Security.Data.EntityFramework.Sqlite, version 1.0.0-alpha14;
* Platformus.WebApplication, version 1.0.0-alpha14.

After that ``dependencies`` section of your project.json file should look like this:

.. code-block:: js
    :emphasize-lines: 8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28

    "dependencies": {
      "Microsoft.AspNetCore.Server.IISIntegration": "1.1.0",
      "Microsoft.AspNetCore.Server.Kestrel": "1.1.0",
      "Microsoft.Extensions.Logging.Console": "1.1.0",
      "Microsoft.NETCore.App": {
        "version": "1.1.0",
        "type": "platform"
      },
      "Platformus.Configurations": "1.0.0-alpha14",
      "Platformus.Configurations.Backend": "1.0.0-alpha14",
      "Platformus.Configurations.Data.EntityFramework.Sqlite": "1.0.0-alpha14",
      "Platformus.Domain.Api": "1.0.0-alpha14",
      "Platformus.Domain.Backend": "1.0.0-alpha14",
      "Platformus.Domain.Data.EntityFramework.Sqlite": "1.0.0-alpha14",
      "Platformus.Domain.Frontend": "1.0.0-alpha14",
      "Platformus.FileManager.Backend": "1.0.0-alpha14",
      "Platformus.FileManager.Data.EntityFramework.Sqlite": "1.0.0-alpha14",
      "Platformus.Forms.Backend": "1.0.0-alpha14",
      "Platformus.Forms.Data.EntityFramework.Sqlite": "1.0.0-alpha14",
      "Platformus.Forms.Frontend": "1.0.0-alpha14",
      "Platformus.Globalization.Backend": "1.0.0-alpha14",
      "Platformus.Globalization.Data.EntityFramework.Sqlite": "1.0.0-alpha14",
      "Platformus.Globalization.Frontend": "1.0.0-alpha14",
      "Platformus.Menus.Backend": "1.0.0-alpha14",
      "Platformus.Menus.Data.EntityFramework.Sqlite": "1.0.0-alpha14",
      "Platformus.Menus.Frontend": "1.0.0-alpha14",
      "Platformus.Security.Backend": "1.0.0-alpha14",
      "Platformus.Security.Data.EntityFramework.Sqlite": "1.0.0-alpha14",
      "Platformus.WebApplication": "1.0.0-alpha14"
    }