Custom Data Sources
===================

To avoid the need for writing a separate endpoint each time we need different data to process the request,
each endpoint can have the data sources defined by a user. For example, if we are using the default endpoint
which returns objects using the views, we may add one more data source to display a weather forecast on the page.

Data source is the C# class that implements the
`IDataSource <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/DataSources/IDataSource.cs#L10>`_ interface.
Endpoints can use the data sources as they (or developer) want. Default endpoint uses them to construct the view model for the views.
Let’s write our own simple data source which will return some hardcoded values.

Create the ``HardcodedValuesDataSource`` class inside the main web application project and implement the ``IDataSource`` interface there
(in order to be able to write custom code in your Platformus-based web application, you can’t use Platformus
as the compiled executable; use it as the NuGet packages instead, or write your own extension project and then put its compiled DLL file inside the extensions folder):

.. code-block:: cs
    :emphasize-lines: 8

    public class HardcodedValuesDataSource : DataSourceBase
    {
      protected override dynamic GetRawData(IRequestHandler requestHandler, DataSource dataSource)
      {
        ExpandoObject viewModel = new ExpandoObject();

        (viewModel as IDictionary<string, dynamic>).Add("Value", "Some hardcoded value from our custom data source.");
        return viewModel;
      }
    }

As you can see, we used the `DataSourceBase <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/DataSources/DataSourceBase.cs#L11>`_
abstract class instead of implementing the ``IDataSource`` interface from scratch. It provides useful methods to manipulate the data source parameters (see below).

Please do not confuse the data source entity
(the `Platformus.Routing.Data.Entities.DataSource <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing.Data.Entities/DataSource.cs#L12>`_ class
which implements the ``IEntity`` interface) and the implementations of the ``IDataSource`` interface (real data sources). Entities are used to describe the data sources
by the users in the backend. They are simple DTO objects, while the real data sources implement some logic. The data source entity contains the ``CSharpClassName`` property,
which actually defines which C# class is used as the real data source.

Now, when our data source class is added, navigate to the backend’s :guilabel:`Development/Endpoints` section, then to the data source list of the Default endpoint,
and create one more data source:

.. image:: /images/advanced/custom_data_sources/1.png

Please note, that our new data source C# class is automatically resolved and added to the drop down list. Click the :guilabel:`Save` button. Data source is created:

.. image:: /images/advanced/custom_data_sources/2.png

All the regular pages now have the ``HardcodedValues`` property inside their view models. (It is only because the default endpoint acts in this way,
but you can implement the endpoint which will process the data sources in a different way).

Let’s update the RegularPage.cshtml view to display the value from our new data source:

.. code-block:: html
    :emphasize-lines: 1

    <p>@Model.HardcodedValues.Value</p>

Run the web application and check the output:

.. image:: /images/advanced/custom_data_sources/3.png

Good. Everything works as expected.

Data Source Parameters and Parameter Groups
-------------------------------------------

As well as the endpoints, data sources support parameters and parameter groups. The implementation is absolutely the same, so please just take a look at
the `one for the endpoints <https://docs.platformus.net/en/latest/advanced/custom_endpoints.html#endpoint-parameters-and-parameter-groups>`_.
Also, please take a look at the `built-in data sources <https://github.com/Platformus/Platformus/tree/master/src/Platformus.Domain/DataSources>`_
to see how they use this feature.