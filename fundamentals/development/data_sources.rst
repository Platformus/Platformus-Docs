.. _data-sources:

Data Sources
============

Each endpoint needs data sources to be able to build a model. Data sources use the specified implementation of the
<https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/DataProviders/IDataProvider.cs#L12>`_
to provide data to the endpoint. You can manage them (create, edit, and delete) from the backend using the
:guilabel:`Data sources` section of every :ref:`endpoint <endpoints>`:

.. image:: /images/fundamentals/development/data_sources/1.png

Each data source has code and data provider C# class name:

.. image:: /images/fundamentals/development/data_sources/2.png

:guilabel:`Code`
~~~~~~~~~~~~~~~~

Code is used as the model property name. So, if you have specified some code,
your model (for example, a view model) will have a property with this name.

:guilabel:`Data provider C# class`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It allows you to specify, which C# class (implementation of the
`IRequestProcessor <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/DataProviders/IDataProvider.cs#L12>`_
interface) will provide data for this data source.

There are few built-in data providers.
`PageObjectDataProvider <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/DataProviders/PageObjectDataProvider.cs#L18>`_
loads the object by its ``URL`` property value.
`ObjectsDataProvider <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/DataProviders/ObjectsDataProvider.cs#L16>`_
loads the objects of the specified class.
`RelatedObjectsDataProvider <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/DataProviders/RelatedObjectsDataProvider.cs#L19>`_
loads the objects that are related to the one, which ``URL`` property value matches current request’s URL.