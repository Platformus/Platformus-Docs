Custom Request Handling
=======================

Custom Default Route Handlers
-----------------------------

The Platformus.Globalization.Frontend package contains the
`UseMvcAction <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Globalization.Frontend/Actions/UseMvcAction.cs#L14>`_ class.
This class `registers <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Globalization.Frontend/Actions/UseMvcAction.cs#L27>`_
the default route (it is done using the features of the underlying ExtCore framework) which is used to handle all the requests in the Platformus-based web application.
It is defined here, because this route might include culture segment (depending on the configuration). Also, this project contains the
`default controller <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Globalization.Frontend/Controllers/DefaultController.cs#L10>`_ itself.

This controller doesn’t generate any response by itself. It looks for the implementations of the
`IDefaultRouteHandler <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Globalization.Frontend/IDefaultRouteHandler.cs#L9>`_ interface
and executes their ``TryHandle()`` method one by one, until it gets the not-null result. If none of the default route handlers returned a not-null result,
the 404 exception is thrown.

Default route handlers might be considered as a middleware which can process the requests. There is the only one implementation of the
``IDefaultRouteHandler`` interface exists in the Platformus from the box: the
`DefaultRouteHandler <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing.Frontend/DefaultRouteHandler.cs#L19>`_ class.
This implementation gets the endpoint resolver service from the DI and gets the endpoint that will handle the request using it. Also,
it performs required security checks.

If you need to handle some requests (and let Platformus to handle other ones as it works by default), just implement the ``IDefaultRouteHandler``
and return not-null result for some particular requests:

.. code-block:: cs
    :emphasize-lines: 6

    public class CustomDefaultRouteHandler : IDefaultRouteHandler
    {
      public IActionResult TryHandle(IRequestHandler requestHandler, string url)
      {
        if (url == "some-url")
          return (requestHandler as Controller).Content("Handled!");

        return null;
      }
    }

Navigate to https://localhost:5000/en/some-url:

.. image:: /images/platformus_website/advanced/custom_request_handling/1.png

You don’t have any object with such URL, but our default route handler worked and you have the response, not 404 error.

Custom Routes
-------------

While the previous solution is a bit limited, you can get the full access to the MVC routing system using the features
of the underlying ExtCore framework. You can implement the ``ExtCore.Mvc.Infrastructure.Actions.IUseMvcAction`` interface
and register as many routes as you need:

.. code-block:: cs
    :emphasize-lines: 7

    public class UseMvcAction : IUseMvcAction
    {
      public int Priority => 1000;

      public void Execute(IRouteBuilder routeBuilder, IServiceProvider serviceProvider)
      {
        routeBuilder.MapRoute(name: "UniqueName", template: "your/template/{anything}", defaults: new { controller = "YourController", action = "YourAction" });
      }
    }