Use as Sources
==============

Use Platformus CMS as the source code only if you consider it as a starting point for your own project and do not need any updates in the future.

1. Create an ASP.NET Core host web application (or use an existing one):

.. image:: /images/getting_started/use_as_sources/1.png

.. image:: /images/getting_started/use_as_sources/2.png

2. Download `Platformus sources <https://github.com/Platformus/Platformus/tree/master/src>`_ from the GitHub.
Copy them into your solution folder.

3. Add dependencies on the following projects to your web application project:

* Platformus.Core.Data.EntityFramework.Sqlite;
* Platformus.Images;
* Platformus.Website.Backend;
* Platformus.Website.Data.EntityFramework.Sqlite;
* Platformus.Website.Frontend;
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
    :emphasize-lines: 3-7
	
    public void ConfigureServices(IServiceCollection services)
    {
      services.Configure<StorageContextOptions>(options =>
        {
          options.ConnectionString = this.configuration.GetConnectionString("Default");
        }
      );
	  
      services.AddPlatformus(this.extensionsPath);
    }

Add the ``applicationBuilder.UsePlatformus()`` extension method call inside the ``Configure`` method:

.. code-block:: cs
    :emphasize-lines: 6
	
    public void Configure(IApplicationBuilder applicationBuilder, IWebHostEnvironment webHostEnvironment)
    {
      if (webHostEnvironment.IsDevelopment())
        applicationBuilder.UseDeveloperExceptionPage();

      applicationBuilder.UsePlatformus();
    }

Don’t forget to include the ``Platformus.WebApplication.Extensions`` namespace in order these extension methods
to be resolved.

4. Execute the Platformus :ref:`database scripts<Database Scripts>`_ on your database.

5. Run your web application and navigate to /backend to configure Platformus.
Use the default "admin@platformus.net" and "admin" credentials to sign in.