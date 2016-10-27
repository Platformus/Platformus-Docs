Tutorial: Create Class
======================

We are going to create a class. Please follow
`this tutorial <http://docs.platformus.net/en/latest/getting_started/tutorial_simple.html>`_ to create
simple Platformus-based web application first. We will use it as a base.

Before we continue you could read more about
`Platformus data model <http://docs.platformus.net/en/latest/fundamentals/data_model.html>`_.

So, according to the `data model <http://docs.platformus.net/en/latest/fundamentals/data_model.html>`_
section, classes describe objects with the members and data sources. Let’s create our own class. Run
your Platformus-based web application and go to the backend, then to the Classes list:

.. image:: /images/tutorial_class/1.png

As you can see there are two classes here: BasePage and Page. Just ignore them for now.

Create Class Form
-----------------

Click the Create class link:

.. image:: /images/tutorial_class/2.png

Name and Pluralized Name Fields
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These two are obvious. Pluralized name is used to name the list of the objects of the class.

Is Abstract Checkbox
~~~~~~~~~~~~~~~~~~~~

Abstract classes can’t be used directly to create the objects, but they can be used as parent classes
for the others. Child classes copy all of the members and data sources from their parent classes.
Currently Platformus supports single inheritance level only. Abstract classes is good idea to avoid
adding the same members (like SEO ones: Title, META description and META keywords) again and again.

Is Standalone Checkbox
~~~~~~~~~~~~~~~~~~~~~~

Objects can be standalone and embedded (this is described in
`data model <http://docs.platformus.net/en/latest/fundamentals/data_model.html>`_ section too). While
standalone object can be accessed via URL (using some specified view), embedded object can only be
used as the part of others.

Default View Name
~~~~~~~~~~~~~~~~~

Each standalone object needs a view in order to be displayed. You can specify the default view name
that will be used for the all of the objects of the given class, but it is still possible to override
that view name in any object directly if you need to use some different view.