.. _endpoints:

Endpoints
=========

The purpose of the endpoints is to take some data provided by the :ref:`data sources <data-sources>`, represent it in some way (HTML, JSON, XML etc.),
and return as the response. They also handle access control and caching. You can manage them (create, edit, and delete) from the backend
using the :guilabel:`Development/Endpoints` section:

.. image:: /images/platformus_website/endpoints/1.png

Please note, that the default ASP.NET routing still works and it is executed before any endpoint.

Each endpoint has name, URL template, position, and other fields:

.. image:: /images/platformus_website/endpoints/2.png

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

Position is important, because the `endpoint resolver <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/Services/Defaults/DefaultEndpointResolver.cs#L16>`_
checks the endpoints one by one, and it will return the first matching endpoint from the list, sorted by position.

.. image:: /images/platformus_website/endpoints/3.png

:guilabel:`Access/Disallow anonymous`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This checkbox allows you to specify whether a user must be authenticated in order to be able to get the response from this endpoint.
Once the checkbox is checked, the :guilabel:`Required permissions` list will appear so you can specify which permissions the user must have.

:guilabel:`Access/Sign in URL`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This URL will be used to redirect user if he must be authenticated or if a required permission is missing.

.. image:: /images/platformus_website/endpoints/4.png

:guilabel:`Request processing/Request processor C# class name`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It allows you to specify, which C# class (implementation of the
`IRequestProcessor <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/RequestProcessors/IRequestProcessor.cs#L15>`_
interface) will process the requests (convert request data and data provided by the data sources to the response). It is very important,
because you can write your own implementations of this interface. You can return HTML (using or not using views), JSON, files, plain text, redirects, or any other content.
There is the only one built-in request processor: the
`DefaultRequestProcessor <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/RequestProcessors/DefaultRequestProcessor.cs#L17>`_
one. It returns views as the ASP.NET controllers (you can specify the view name).

Please note that the endpoints process requests using the request processors, they do not (and should not) provide data for the responses.
In other words, they take prepared data and represent it in some way (HTML, JSON etc.). Data is provided to the endpoints by :ref:`data sources <data-sources>`.
Each endpoint can have different data sources at the same time.

.. image:: /images/platformus_website/endpoints/5.png

:guilabel:`Response caching/Response cache C# class name`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It allows you to specify, which C# class (implementation of the
`IResponseCache <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/ResponseCaches/IResponseCache.cs#L14>`_
is used to cache the endpoint response. There are several built-in `implementations of this interface <https://github.com/Platformus/Platformus/tree/master/src/Platformus.Website.Frontend/ResponseCaches>`_,
but you can write your own ones.