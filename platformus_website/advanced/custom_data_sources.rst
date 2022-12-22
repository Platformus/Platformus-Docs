.. _custom-data-providers:

Custom Data Sources
===================

As we know, data providers are used by :ref:`data sources <data-sources>` to provide :ref:`endpoints <endpoints>` with data.
It is a regular C# class that implements the `IDataProvider <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/DataProviders/IDataProvider.cs#L16>`_
interface. There are several `built-in data providers <https://github.com/Platformus/Platformus/tree/master/src/Platformus.Website.Frontend/DataProviders>`_,
but all of them work with the :ref:`objects <objects>`. Let’s create a custom one that will just provide a hardcoded text.

Create the ``HardcodedValuesDataProvider`` class inside the main web application project and implement the ``IDataProvider`` interface:

.. code-block:: cs
    :emphasize-lines: 13

    public class MyDataProvider : IDataProvider
    {
      public string Description => "Provides the hardcoded values.";

      public IEnumerable<ParameterGroup> ParameterGroups => new ParameterGroup[] { };

      public async Task<dynamic> GetDataAsync(HttpContext httpContext, DataSource dataSource)
      {
        ExpandoObjectBuilder expandoObjectBuilder = new ExpandoObjectBuilder();

        expandoObjectBuilder.AddProperty("Value", "Some hardcoded value from our custom data source.");
        return expandoObjectBuilder.Build();
      }
    }

Now, when our data provider class is added, navigate to the backend’s :guilabel:`Development/Endpoints` section, then to the data source list of the Default endpoint,
and create one more data source:

.. image:: /images/platformus_website/advanced/custom_data_sources/1.png

Please note, that our new data provider C# class is automatically resolved and added to the drop down list. Click the :guilabel:`Save` button. Data source is created:

.. image:: /images/platformus_website/advanced/custom_data_sources/2.png

All the regular pages now have the ``Hardcoded`` property inside their view models (thanks to the
`DefaultRequestProcessor <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/RequestProcessors/DefaultRequestProcessor.cs#L17>`_
request processor; your own request processor might act in a different way to process provided data).

Let’s update the RegularPage.cshtml view to display the value from our new data source:

.. code-block:: html
    :emphasize-lines: 1

    <p>@Model.Hardcoded.Value</p>

Run the web application and check the output:

.. image:: /images/platformus_website/advanced/custom_data_sources/3.png

Good. Everything works as expected.

Data Source Parameters and Parameter Groups
-------------------------------------------

As well as the form handlers and endpoints, data providers support parameters and parameter groups. The implementation is absolutely the same,
so please just take a look at the :ref:`endpoints <custom-endpoints>` for the sample. Also, please take a look at the
`built-in data providers <https://github.com/Platformus/Platformus/tree/master/src/Platformus.Website.Frontend/DataProviders>`_
to see how they get the parameter values.