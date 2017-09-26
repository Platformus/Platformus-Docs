Use as Sources
==============

This option gives you full control over Platformus and your web application. Also it is the way to develop
Platformus itself. Please keep in mind that compilation takes longer in this case, so include only the sources
of the projects you really need to modify.

1. Create an ASP.NET Core web application (or use an existing one):

.. image:: /images/getting_started/use_as_sources/1.png

.. image:: /images/getting_started/use_as_sources/2.png

2. Download `Platformus sources <https://github.com/Platformus/Platformus/tree/master/src>`_ from the GitHub.
Copy them into your solution.

3. Add dependencies  on the following projects to your web application project:

* Platformus.Configurations.Backend;
* Platformus.Configurations.Data.EntityFramework.Sqlite;
* Platformus.Designers.Backend;
* Platformus.Domain.Api;
* Platformus.Domain.Backend;
* Platformus.Domain.Data.EntityFramework.Sqlite;
* Platformus.Domain.Frontend;
* Platformus.FileManager.Backend;
* Platformus.FileManager.Data.EntityFramework.Sqlite;
* Platformus.Forms.Backend;
* Platformus.Forms.Data.EntityFramework.Sqlite;
* Platformus.Forms.Frontend;
* Platformus.Globalization.Backend;
* Platformus.Globalization.Data.EntityFramework.Sqlite;
* Platformus.Globalization.Frontend;
* Platformus.Menus.Backend;
* Platformus.Menus.Data.EntityFramework.Sqlite;
* Platformus.Menus.Frontend;
* Platformus.Routing.Backend;
* Platformus.Routing.Data.EntityFramework.Sqlite;
* Platformus.Routing.Frontend;
* Platformus.Security.Backend;
* Platformus.Security.Data.EntityFramework.Sqlite;
* Platformus.WebApplication.

4. Open your ``Startup`` class.

Add the ``services.AddPlatformus()`` extension method call inside the ``ConfigureServices`` method:

.. code-block:: cs
    :emphasize-lines: 3
	
	public void ConfigureServices(IServiceCollection services)
    {
      services.AddPlatformus();
    }

Add the ``StorageContextOptions`` options class configuration inside the ``ConfigureServices`` method
in order to provide the connection string (of course, you should take it from the application settings):

.. code-block:: cs
    :emphasize-lines: 4-8
	
	public void ConfigureServices(IServiceCollection services)
    {
      services.AddPlatformus(this.extensionsPath);
      services.Configure<StorageContextOptions>(options =>
        {
          options.ConnectionString = this.configurationRoot.GetConnectionString("Default");
        }
      );
    }

Add the ``applicationBuilder.UsePlatformus()`` extension method call inside the ``Configure`` method:

.. code-block:: cs
    :emphasize-lines: 8
	
	public void Configure(IApplicationBuilder applicationBuilder, IHostingEnvironment hostingEnvironment)
    {
      if (hostingEnvironment.IsDevelopment())
      {
        applicationBuilder.UseDeveloperExceptionPage();
      }

      applicationBuilder.UsePlatformus();
    }

Don’t forget to include the ``Platformus.WebApplication.Extensions`` namespace in order these extension methods
to be resolved.

5. Run your web application and navigate to /backend to configure Platformus.