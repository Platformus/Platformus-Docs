Tutorial: Creating Custom Extension
===================================

When you create a Platformus-based application, unless it's something quite simple, you’ll probably need to create your own Platformus extension.
It will contain everything that is related to your app (entities, models, DTOs, services, APIs, UI etc.) to keep it separated and independent from the basic CMS.

Creating an extension is simple. We will go through all the aspects and create a sample mobile app backend with authentication
(phone number validation using a fake code from SMS), categories and products API, and corresponding admin panel sections to manage categories and products etc.

Preparing the Solution
----------------------

Let’s start from the beginning. First, please follow the :ref:`Using as the NuGet Packages <tutorial-basic-content-management>` tutorial
to create an empty ASP.NET Core Platformus-based web application but keep only the Platformus.WebApplication package dependency as we do not need the others.
