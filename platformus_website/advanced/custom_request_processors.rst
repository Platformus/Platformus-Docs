.. _custom-request-processors:

Custom Endpoints
================

As we have discussed in the `Introduction <https://docs.platformus.net/en/latest/introduction/index.html>`_ and
`Getting Started\Tutorial: Basic Content Management <https://docs.platformus.net/en/latest/getting_started/tutorial_basic_content_management.html>`_ articles,
endpoints handle the HTTP requests that come to a Platformus-based web application. When request comes, particular endpoint is resolved by the implementation of the
`IEndpointResolver <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/EndpointResolvers/IEndpointResolver.cs#L10>`_ interface,
depending on the URL template (it is behavior of the
`default interface implementation <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/EndpointResolvers/DefaultEndpointResolver.cs#L13>`_,
but you can change it too). When the suitable endpoint is selected and instantiated, it processes the request and returns an action result.

Platformus has the only one built-in implementation of the
`IEndpoint <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/Endpoints/IEndpoint.cs#L11>`_ interface:
the `DefaultEndpoint <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Domain.Frontend/Endpoints/DefaultEndpoint.cs#L15>`_ class.
It is located inside the Domain extension (the Platformus.Domain.Frontend assembly) and it knows about objects and properties, and returns the views.

Let’s implement our own endpoint, which will return some JSON for us. Create the ``ApiEndpoint`` class inside the main web application project
and implement the ``IEndpoint`` interface there (in order to be able to write custom code in your Platformus-based web application, you can’t use Platformus
as the compiled executable; use it as the NuGet packages instead, or write your own extension project and then put its compiled DLL file inside the extensions folder):

.. code-block:: cs
    :emphasize-lines: 5

    public class ApiEndpoint : EndpointBase
    {
      protected override IActionResult GetActionResult(IRequestHandler requestHandler, Endpoint endpoint, IEnumerable<KeyValuePair<string, string>> arguments)
      {
        return (requestHandler as Controller).Json(new { x = 10, y = true });
      }
    }

As you can see, we used the `EndpointBase <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/Endpoints/EndpointBase.cs#L12>`_
abstract class instead of implementing the ``IEndpoint`` interface from scratch. It provides useful methods to manipulate the endpoint parameters and URL arguments
that come from the endpoint resolver (see below).

Please do not confuse the endpoint entity
(the `Platformus.Routing.Data.Entities.Endpoint <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing.Data.Entities/Endpoint.cs#L12>`_ class
which implements the ``IEntity`` interface) and the implementations of the ``IEndpoint`` interface (real endpoints). Entities are used to describe the endpoints
by the users in the backend. They are simple DTO objects, while the real endpoints implement some logic. The endpoint entity contains the ``CSharpClassName`` property,
which actually defines which C# class is used as the real endpoint.

Now, when our endpoint class is added, navigate to the backend’s :guilabel:`Development/Endpoints` section and create one more endpoint:

.. image:: /images/platformus_website/advanced/custom_endpoints/1.png

Please note, that our new endpoint C# class is automatically resolved and added to the drop down list. Click the :guilabel:`Save` button. Endpoint is created:

.. image:: /images/platformus_website/advanced/custom_endpoints/2.png

Now navigate to /en/api and our new endpoint will process the request:

.. image:: /images/platformus_website/advanced/custom_endpoints/3.png

Good. Everything works as expected.

Endpoint Parameters and Parameter Groups
----------------------------------------

Now let’s assume that we want to make it possible to specify the data format for our API output.
It can be done using the endpoint parameters. Override the ``ParameterGroups`` property in our endpoint class:

.. code-block:: cs
    :emphasize-lines: 1

    public override IEnumerable<EndpointParameterGroup> ParameterGroups => new EndpointParameterGroup[]
    {
      new EndpointParameterGroup(
        "Output",
        new EndpointParameter("DataFormat", "Data format", new Option[] { new Option("JSON"), new Option("XML") }, "radioButtonList", null, true)
      )
    };

This property just returns the enumeration of the parameter groups. Each of them can contain enumeration of the parameters.
Parameters have client-side JavaScript editors (4th constructor argument).  The supported JavaScript editor class names are:
``textBox``, ``numericTextBox``, ``checkbox``, ``radioButtonList``, and ``dropDownList``.

Let’s override also the ``Description`` property:

.. code-block:: cs
    :emphasize-lines: 1

    public override string Description => "Returns data using the specified data format.";

It simply contains some text description of the endpoint which will be shown to a user in the backend.

Now edit our endpoint in the backend:

.. image:: /images/platformus_website/advanced/custom_endpoints/4.png

Now the endpoint group with the parameter is displayed. Let’s see how to get the selected value from the code:

.. code-block:: cs
    :emphasize-lines: 3

    protected override IActionResult GetActionResult(IRequestHandler requestHandler, Endpoint endpoint, IEnumerable<KeyValuePair<string, string>> arguments)
    {
      if (this.GetStringParameterValue("DataFormat") == "JSON")
        return (requestHandler as Controller).Json(new { x = 10, y = true });

      return (requestHandler as Controller).Content("<x>10</x><y>true</y>");
    }

If you change the data format in the backend, the endpoint output will also be changed:

.. image:: /images/platformus_website/advanced/custom_endpoints/5.png

URL arguments
-------------

Endpoint URL templates support URL arguments (similar way it is done in MVC routes). Change the URL template of our endpoint next way:
``{prefix}api{suffix}/{id}``.

Now you can get these URL arguments from the endpoint class like this:

.. code-block:: cs
    :emphasize-lines: 1

    string prefix = arguments.FirstOrDefault(a => a.Key == "prefix").Value;

For example, for the URL like ``/en/xxxapiyyy/100`` ``prefix`` argument value will be ``xxx``, ``suffix`` will be ``yyy``,
and ``id`` will be ``100``.