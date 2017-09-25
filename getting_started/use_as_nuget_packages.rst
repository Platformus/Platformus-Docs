Use as NuGet Packages
=====================

1. Create an ASP.NET Core web application (or use an existing one):

.. image:: /images/getting_started/use_as_nuget_packages/1.png

.. image:: /images/getting_started/use_as_nuget_packages/2.png

2. Open NuGet Package Manager and add dependencies on the following Platformus packages:

.. image:: /images/getting_started/use_as_nuget_packages/3.png

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

Or you can add them manually by editing .csproj file of your web application project:

.. code-block:: xml
    :emphasize-lines: 2-25

    <ItemGroup>
      <PackageReference Include="Platformus.Configurations.Backend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Configurations.Data.EntityFramework.Sqlite" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Designers.Backend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Domain.Api" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Domain.Backend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Domain.Data.EntityFramework.Sqlite" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Domain.Frontend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.FileManager.Backend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.FileManager.Data.EntityFramework.Sqlite" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Forms.Backend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Forms.Data.EntityFramework.Sqlite" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Forms.Frontend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Globalization.Backend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Globalization.Data.EntityFramework.Sqlite" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Globalization.Frontend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Menus.Backend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Menus.Data.EntityFramework.Sqlite" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Menus.Frontend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Routing.Backend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Routing.Data.EntityFramework.Sqlite" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Routing.Frontend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Security.Backend" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.Security.Data.EntityFramework.Sqlite" Version="1.0.0-beta1" />
      <PackageReference Include="Platformus.WebApplication" Version="1.0.0-beta1" />
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

4. Run your web application and navigate to /backend to configure Platformus.