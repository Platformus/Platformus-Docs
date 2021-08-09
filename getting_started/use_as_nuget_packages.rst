Use as the NuGet Packages
=========================

To use Platformus CMS as the NuGet packages create a host web application, add dependencies on the corresponding packages,
and write application-specific code. You can extend the built-in features and modify the default behavior using the Platformus public API.

1. Create an ASP.NET Core web application (or use an existing one):

.. image:: /images/getting_started/use_as_nuget_packages/1.png

.. image:: /images/getting_started/use_as_nuget_packages/2.png

2. Open NuGet Package Manager and add dependencies on the following Platformus packages:

.. image:: /images/getting_started/use_as_nuget_packages/3.png

* Platformus.Core.Data.EntityFramework.Sqlite;
* Platformus.Images;
* Platformus.Website.Backend;
* Platformus.Website.Data.EntityFramework.Sqlite;
* Platformus.Website.Frontend;
* Platformus.WebApplication.

Or you can add them manually by editing .csproj file of your web application project:

.. code-block:: xml
    :emphasize-lines: 2-7

    <ItemGroup>
      <PackageReference Include="Platformus.Core.Data.EntityFramework.Sqlite" Version="2.4.0" />
      <PackageReference Include="Platformus.Images" Version="2.4.0" />
      <PackageReference Include="Platformus.Website.Backend" Version="2.4.0" />
      <PackageReference Include="Platformus.Website.Data.EntityFramework.SqlServer" Version="2.4.0" />
      <PackageReference Include="Platformus.Website.Frontend" Version="2.4.0" />
      <PackageReference Include="Platformus.WebApplication" Version="2.4.0" />
    </ItemGroup>

3. Open your ``Startup`` class.

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

Don’t forget to include the ``Platformus.WebApplication.Extensions`` namespace in order these extension methods to be resolved.

4. Execute Platformus `database scripts <https://platformus.readthedocs.io/en/latest/getting_started/database_scripts.html>`_ on your database.

5. Run your web application and navigate to /backend to configure Platformus.
Use the default "admin@platformus.net" and "admin" credentials to sign in.