Tutorial: Creating a Custom Extension
=====================================

When you create a Platformus-based application, unless it's something quite simple, you’ll probably need to create your own Platformus extension.
It will contain everything that is related to your app (entities, models, DTOs, services, APIs, UI etc.) to keep it separated and independent from the basic CMS.

Creating an extension is simple. We will go through all the aspects and create a sample mobile app backend with authentication
(phone number validation using a fake code from SMS), categories and products API, and corresponding admin panel sections to manage categories and products etc.

Preparing the Solution
----------------------

Let’s start from the beginning. First, please follow the :ref:`Using as the NuGet Packages <using-as-the-nuget-packages>` tutorial
to create an empty ASP.NET Core Platformus-based web application but keep only the Platformus.WebApplication and Platformus.Core packages dependencies
as we do not need the others.

Recommended Solution Structure
------------------------------

You can organize your code in an any way you want, but it is recommended to use the following solution structure.

WebApplication
~~~~~~~~~~~~~~

It is the executable main web application. It provides logging, configuration, stores static content, initializes Platformus.

Shouldn’t be referenced from another projects.

WebApplication.Frontend
~~~~~~~~~~~~~~~~~~~~~~~

Contains everything related to the frontend: DTOs and view models, APIs with authentication configuration and validation rules, views, pages etc.

Shouldn’t be referenced from other projects except the WebApplication one.

WebApplication.Backend
~~~~~~~~~~~~~~~~~~~~~~

Contains everything related to the backend (admin panel): DTO and view models, controllers, views, pages etc.

Shouldn’t be referenced from other projects except the WebApplication one.

WebApplication.Domain.Models
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Contains only the domain models.

WebApplication.Domain.Abstractions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Contains the domain service interfaces (for those models which do not use and need to replace the generic domain service provided by the Magicalizer).

WebApplication.Domain.Defaults
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Contains the domain service implementations (for those models which do not use and need to replace the generic domain service provided by the Magicalizer).

WebApplication.Data.Entities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Contains only the entities.

WebApplication.Data.Abstractions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Contains the repository interfaces (for those entities which do not use and need to replace the generic repository provided by the Magicalizer).

WebApplication.Data.EntityFramework.SqlServer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Contains the repository implementations for the specific database (for those entities which do not use and need to replace
the generic repository provided by the Magicalizer) and the Entity Framework context configuration.