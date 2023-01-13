.. _custom-extension:

Custom Extensions
=================

It is not difficult to develop a custom Platformus CMS extension. You can add dependency on any C# project in your Platformus-based application
like in any other ASP.NET app, controllers and other features will work as you expect. But Platformus provides you with some public API,
so you can extend it, add backend (admin panel) sections, security policies etc.

There are 2 main purposes to have custom Platformus extensions.

1. You can have all your code in the isolated projects, so CMS itself can be updated independently.
2. You can decrease development time reusing code and combining your apps from the existing parts. It could be useful when you develop a lot of apps
and have standard approaches of fixing standard tasks. For example, most of the apps have authentication part, some Firebase cloud messaging features.
Many of them also have chats on SignalR.

As Platformus CMS is built on top of the `ExtCore framework <https://extcore.net/>`_, you can use your custom extension in the different ways:
as NuGet packages, source code, or even DLL-files.

.. toctree::
   :titlesonly:

   backend_dashboard_widgets
   backend_menu
   backend_styles_scripts
   embedded_resources