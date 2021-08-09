Use as Sources
==============

To use Platformus CMS as the source code create a host web application,
copy the Platformus source code to the solution folder and add corresponding project dependencies.
Please keep in mind that compilation takes longer in this case, so include only the sources of the projects you really need.

1. Create an ASP.NET Core web application (or use an existing one):

.. image:: /images/getting_started/use_as_sources/1.png

.. image:: /images/getting_started/use_as_sources/2.png

2. Download `Platformus sources <https://github.com/Platformus/Platformus/tree/master/src>`_ from the GitHub.
Copy them into your solution.

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

4. Execute Platformus `database scripts <https://platformus.readthedocs.io/en/latest/getting_started/database_scripts.html>`_ on your database.

5. Run your web application and navigate to /backend to configure Platformus.
Use the default "admin@platformus.net" and "admin" credentials to sign in.