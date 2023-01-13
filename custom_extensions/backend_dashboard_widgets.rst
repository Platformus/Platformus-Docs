.. _backend-menu:

Backend Dashboard Widgets
=========================

Most of the apps have some key metrics, analytics, or statistics that should be available in a fast and convenient way.
It could be number of the registered users or orders for the last week, sales amount etc.

The home page of the Platformus CMS backend (admin panel) is a dashboard where you can add your own widgets.
Each widget is a regular `view component <https://learn.microsoft.com/en-us/aspnet/core/mvc/views/view-components>`_,
so it has its own view and can look and behave in any way.

To add your view component(s) to the dashboard you need to implement the
`IMetadata <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/IMetadata.cs#L9>`_ interface.
It is preferable to use the `MetadataBase <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/MetadataBase.cs#L9>`_
class to be able to override only the methods you want:

.. code-block:: cs
    :emphasize-lines: 5

    public class MyMetadata : MetadataBase
    {
      public override IEnumerable<DashboardWidget> GetDashboardWidgets(HttpContext httpContext)
      {
        return new DashboardWidget[]
        {
          new DashboardWidget("MyViewComponent", 1000)
        };
      }
    }

This file can be placed anywhere in the project, it will be resolved automatically by the
`default implementation <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/Providers/DefaultDashboardWidgetsProvider.cs#L11>`_ of the
`IDashboardWidgetsProvider <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/Providers/IDashboardWidgetsProvider.cs#L9>`_ interface.

Let’s look at the `DashboardWidget <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/DashboardWidget.cs#L6>`_ class’s properties.

``ViewComponentName`` is the view component name.

``Position`` is used to sort the widgets. Widgets with a lower position are placed higher.