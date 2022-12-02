.. _endpoints:

Endpoints
=========

Endpoints are used to handle the requests to a Platformus-based web application. You can manage them
(create, edit, and delete) from the backend using the :guilabel:`Development/Endpoints` section:

.. image:: /images/fundamentals/development/endpoints/1.png

Each endpoint has name, URL template, position, and other fields:

.. image:: /images/fundamentals/development/endpoints/2.png

.. image:: /images/fundamentals/development/endpoints/3.png

:guilabel:`General/Name`
~~~~~~~~~~~~~~~~~~~~~~~~

Name is used only in the endpoint list to identify endpoints.

:guilabel:`General/URL template`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

URL template is used by the implementation of the
`IEndpointResolver <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/Services/Abstractions/IEndpointResolver.cs#L9>`_
interface to select the endpoint which should process current request (see below).

:guilabel:`General/Position`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Position is important, because endpoint resolver checks the endpoints one by one, and it will return the first
matching endpoint from the list, sorted by position.

:guilabel:`General/Disallow anonymous`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This checkbox allows you to specify whether a user must be authenticated
in order to be able to get the response from this endpoint. On the :guilabel:`Required permissions` tab you can specify
which permissions the user must have.

:guilabel:`General/Sign in URL`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This URL will be used to redirect user if he must be authenticated or if a required permission is missing.

.. image:: /images/fundamentals/development/endpoints/4.png

:guilabel:`Request processing/Request processor C# class name`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It allows you to specify, which C# class (implementation of the
`IRequestProcessor <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/RequestProcessors/IRequestProcessor.cs#L12>`_
interface) will process the requests. It is very important, because you can write your own implementations of this interface
and process the requests in any way you want. You can return views, JSON, files, plain text, redirects, or any other content.
There is the only one built-in request processor: the
`DefaultRequestProcessor <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/RequestProcessors/DefaultRequestProcessor.cs#L18>`_
one. It returns views (you can specify the view name).

If we talk about the views, endpoint should provide some information that a view needs using the view model.
Endpoint creates and initializes a view model using the data sources. Each endpoint can have different :ref:`data sources <data-sources>`.

.. image:: /images/fundamentals/development/endpoints/5.png

:guilabel:`Response caching/Response cache C# class name`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It allows you to specify, which C# class (implementation of the
`IResponseCache <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/ResponseCaches/IResponseCache.cs#L10>`_
is used to cache the endpoint response. There are several built-in `implementations of this interface <https://github.com/Platformus/Platformus/tree/master/src/Platformus.Website.Frontend/ResponseCaches>`_,
but you can write your own ones.