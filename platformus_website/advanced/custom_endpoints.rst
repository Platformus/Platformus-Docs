.. _custom-endpoints:

Custom Endpoints
================

As we know, :ref:`endpoints <endpoints>` process the requests and prepare responses using the data provided by the :ref:`data sources <data-sources>`.
Endpoints use the implementation of the `IRequestProcessor <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/RequestProcessors/IRequestProcessor.cs#L15>`_
interface for that. It can return any ``IActionResult``. The idea is that by changing the request processor class you can represent data in a different way.
That’s why the request processor shouldn’t provide data itself but use the one provided with data sources.

The only one built-in implementation of the `IRequestProcessor <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/RequestProcessors/IRequestProcessor.cs#L15>`_
interface (the `DefaultRequestProcessor <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/RequestProcessors/DefaultRequestProcessor.cs#L17>`_
class) returns Razor views with the view model combined from the data provided by the data sources. Let’s create our own request processor which will return JSON instead:

.. code-block:: cs
    :emphasize-lines: 13

    public class MyRequestProcessor : IRequestProcessor
    {
      public IEnumerable<ParameterGroup> ParameterGroups => new ParameterGroup[] { };
      public string Description => "Returns data as JSON.";

      public async Task<IActionResult> ProcessAsync(HttpContext httpContext, Platformus.Website.Data.Entities.Endpoint endpoint)
      {
        dynamic viewModel = await this.CreateViewModelAsync(httpContext, endpoint);

        if (viewModel == null)
          return null;

        return new JsonResult(viewModel);
      }

      private async Task<dynamic> CreateViewModelAsync(HttpContext httpContext, Platformus.Website.Data.Entities.Endpoint endpoint)
      {
        ExpandoObjectBuilder expandoObjectBuilder = new ExpandoObjectBuilder();

        foreach (DataSource dataSource in endpoint.DataSources)
        {
          dynamic viewModel = await this.GetDataProvider(dataSource).GetDataAsync(httpContext, dataSource);

          if (viewModel == null)
            return null;

          expandoObjectBuilder.AddProperty(dataSource.Code, viewModel);
        }

        return expandoObjectBuilder.Build();
      }

      private IDataProvider GetDataProvider(DataSource dataSource)
      {
        return StringActivator.CreateInstance<IDataProvider>(dataSource.DataProviderCSharpClassName);
      }
    }

Now, when our request processor class is added, navigate to the backend’s :guilabel:`Development/Endpoints` section and change the default endpoint's
request processor C# class name:

.. image:: /images/platformus_website/advanced/custom_endpoints/1.png

Please note, that our new request processor C# class is automatically resolved and added to the drop-down list. Click the :guilabel:`Save` button.

Now navigate to /en/about and our new request processor will process the request:

.. image:: /images/platformus_website/advanced/custom_endpoints/2.png

Good. Everything works as expected.

Endpoint Parameters and Parameter Groups
----------------------------------------

Now let’s assume that we want to make it possible to specify the data format for our request processor output.
It can be done using the parameters. Override the ``ParameterGroups`` property in our endpoint class:

.. code-block:: cs
    :emphasize-lines: 1

    public IEnumerable<ParameterGroup> ParameterGroups => new ParameterGroup[]
    {
      new ParameterGroup(
        "Serialization",
        new Parameter(
          "Format",
          "Format",
          ParameterEditorCodes.RadioButtonList,
          new Option[] {
            new Option("JSON", "json"),
            new Option("XML", "xml")
          }
        )
      )
    };

This property just returns the parameter groups. Each of them can contain different parameters defined by developer.
When user selects the request processor C# class, these parameters will be available for him. Parameters can have different editor types.
All the built-in ones are defined inside the
`ParameterEditorCodes <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core/Constants/ParameterEditorCodes.cs#L9>`_ enum,
but you can also add your own ones. Using the parameter's code, you will be able to get the value entered by a user.

Let’s update also the ``Description`` property to indicate that now we can return either JSON or XML:

.. code-block:: cs
    :emphasize-lines: 1

    public override string Description => "Returns data as JSON or XML.";

Description is also presented to a user when the request processor is selected.

Now open our endpoint in the backend one more time:

.. image:: /images/platformus_website/advanced/custom_endpoints/3.png

The request processor parameter is displayed. Let’s see how to get and use the selected value from the code:

.. code-block:: cs
    :emphasize-lines: 8

    public async Task<IActionResult> ProcessAsync(HttpContext httpContext, Platformus.Website.Data.Entities.Endpoint endpoint)
    {
      dynamic viewModel = await this.CreateViewModelAsync(httpContext, endpoint);

      if (viewModel == null)
        return null;

      string format = new ParametersParser(endpoint.RequestProcessorParameters).GetStringParameterValue("Format");

      if (format == "json")
        return new JsonResult(viewModel);

      XDocument document= new XDocument(
        new XElement("someKey", "Some value")
      );
      
      return new ContentResult() { Content = document.ToString(), ContentType = "application/xml" };
    }

Please note that we only use the hardcoded XML here, because converting dynamic object into an XML might look difficult and isn’t a subject of the article.

Now if you change the data format in the backend, the endpoint output will also be changed:

.. image:: /images/platformus_website/advanced/custom_endpoints/4.png