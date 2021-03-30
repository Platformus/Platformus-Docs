Endpoints
=========

Endpoints are used to handle the requests to a Platformus-based web application. You can manage them
(add, edit, and delete) from the backend using the :guilabel:`Development/Endpoints` section:

.. image:: /images/fundamentals/development/endpoints/1.png

Each endpoint has name, URL template, position, and few other fields:

.. image:: /images/fundamentals/development/endpoints/2.png

Name is used only in the endpoint list. URL template is used by the implementation of the
`IEndpointResolver <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/EndpointResolvers/IEndpointResolver.cs#L10>`_
interface to select the endpoint which should process current request (see below).
Position is important, because endpoint resolver checks the endpoints one by one, and it will return the first
matching endpoint from the list, sorted by position.

The :guilabel:`Disallow anonymous` checkbox allows you to specify, whether a user must be authenticated
in order to be able to get the response from this endpoint. On the :guilabel:`Permissions` tab you can specify
which permissions the user must have and where it should be redirected if it doesn’t have any required permission.

The :guilabel:`C# class name` drop down list allows you to specify, which C# class (implementation of the
`IEndpoint <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/Endpoints/IEndpoint.cs#L11>`_
interface) will handle the requests. It is very important, because you can write your own implementations of this interface
and handle the requests in any way you want. You can return views, JSON, files, plain text, redirects, or any other content.
There is the only one built-in endpoint: the
`DefaultEndpoint <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Domain.Frontend/Endpoints/DefaultEndpoint.cs#L15>`_
class. It returns views (you can specify the view name) and supports caching.

If we are talking about the views, endpoint should provide any information a view needs using the view model.
Endpoint creates and initializes a view model using the data sources. Each endpoint can have different data sources:

.. image:: /images/fundamentals/development/endpoints/3.png

Data source is a C# class too. It must implement the
`IDataSource <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/DataSources/IDataSource.cs#L10>`_
interface. You can implement this interface in your own classes and return any data you want.

There are few built-in data sources. ``PageDataSource`` loads the object by its ``URL`` property value.
``ObjectsDataSource`` loads the objects of the specified class. Also, it supports filtegin, sorting, and paging.
``PrimaryObjectsDataSource`` and ``ForeignObjectsDataSource`` load the objects that are related to the one,
which ``URL`` property value matches current request’s URL (these both support filtegin, sorting, and paging too).

Each data source has code and C# class name:

.. image:: /images/fundamentals/development/endpoints/4.png

While C# class name is clear for now, code is used as the view model property name. So if you have specified some code,
your view model will have a property with this name.

Both endpoints and data sources can have parameters. These parameters are specified by a developer and
can have different types and client-side JavaScript editors. Developers can add their own parameter editors.

You can read more about custom `endpoints <https://docs.platformus.net/en/latest/advanced/custom_endpoints.html>`_
and `data sources <https://docs.platformus.net/en/latest/advanced/custom_data_sources.html>`_ in the
`advanced <https://docs.platformus.net/en/latest/advanced/index.html>`_ section.