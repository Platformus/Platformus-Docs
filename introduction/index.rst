Introduction
============

Platformus is complex and multipurpose content management system. You can describe and store your content,
and it is totally separated from its representation, so you can represent it using the views, API,
or any other way you want.

It can run on Linux, Mac, and Windows (also is can run on Azure cloud). It supports different storage types
(PostgreSQL, SQLite, SQL Server, Azure SQL Database). It is modular, multilingual and multicultural.
And it is open-source and absolutely free.

Data Model
----------

The Platformus data model is described by the classes and members. The data itself is represented by the objects,
properties, and relations (very similar to the way it is done in the popular programming languages).
There are also other types of the content, like menus, forms, files etc.

Requests Handling
-----------------

By default, all the requests that come to a Platformus-based web application are handled by the endpoints
(from the box, Platformus responds with 404 response code to any HTTP request, because there are no endpoints configured;
you can change the built-in way requests are handled in the Platformus too).

Endpoint specifies the URL pattern it matches (the same way it is done in MVC routes, so you can specify {*url} pattern
that will match all the URLs; it also supports the URL parameters) and the C# class (implementation of the
`IEndpoint <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/Endpoints/IEndpoint.cs#L11>`_ interface)
that will process the requests. This class will receive the URL parameters and must return an IActionResult object
(it might be a view, JSON, file, or any other type of response that is supported by the HTTP). The particular endpoint is selected
by the registered implementation (you can also change it) of the
`IEndpointResolver <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/EndpointResolvers/IEndpointResolver.cs#L10>`_
interface at the time of the request.

Each endpoint can have parameters with the different user-defined client-side JavaScript editors. They are specified
by the corresponding C# class. For example, the
`DefaultEndpoint <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Domain.Frontend/Endpoints/DefaultEndpoint.cs#L15>`_
class (which returns views) has two parameters: ViewName and UseCaching. Of course, you can easily write your own endpoints.

If the endpoint needs an additional data in order to process the requests, it can be provided using the data sources.
All data sources are the C# classes that implements the
`IDataSource <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/DataSources/IDataSource.cs#L10>`_
interface (you can write your own ones). You can specify which data sources should be used with the given endpoint
to construct the single piece of data it can use (and pass to a view as the view model for example).
Platformus contains some built-in data sources that allows to load objects by classes, by relations, to use filtering, sorting, and paging.
As well as the endpoints, the data sources can have parameters.