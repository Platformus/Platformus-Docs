Tutorial: Create Class
======================

We are going to create a class. Please follow
`this tutorial <http://docs.platformus.net/en/latest/getting_started/tutorial_simple.html>`_ to create
simple Platformus-based web application first. We will use it as a base.

So, according to the `data model <http://docs.platformus.net/en/latest/fundamentals/data_model.html>`_
section, classes describe objects with the members and data sources. Let’s create our own class. Run
your Platformus-based web application and go to the backend, then to the Classes list:

.. image:: /images/tutorial_class/1.png

As you can see there are two classes here: BasePage and Page. Just ignore them for now.

Create Class
------------

Click the Create class link and fill the Create class form as below:

.. image:: /images/tutorial_class/2.png

Parent Class (Abstract Only) Drop Down List
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The abstract class to copy members and data sources from.

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

Now click the Save button. Our class is created:

.. image:: /images/tutorial_class/3.png

Create Member
-------------

Click the Members link in the our class row. We can see the empty list:

.. image:: /images/tutorial_class/4.png

Now click the Create member link and fill the General tab of the Create member form as below:

.. image:: /images/tutorial_class/5.png

Tab Drop Down List
~~~~~~~~~~~~~~~~~~

Classes might be huge, with large number of members. You can group property editors by the different
tabs to make the object editing process more comfortable.

Code Field
~~~~~~~~~~

Code is used to get the property values.

Name Field
~~~~~~~~~~

This one is obvious.

Position Field
~~~~~~~~~~~~~~

Position defines the order on the edit object page.

And Property tab of the Create member form should look like:

.. image:: /images/tutorial_class/6.png

Property Data Type Drop Down List
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Property data type defines the editor that will be used to edit object property value. You can add
your own data types.

Is Property Localizable Checkbox
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

By default properties are not localizable. It means that their value (or content) does not depend on
the selected culture. Localizable properties have separate editor for each of the cultures, so user
can specify different values for the different cultures.

Is Property Visible in List Checkbox
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can display values of the specific properties in the object lists by setting this checkbox. It should
be set for general properties like name etc.

Now click the Save button. Our member is created:

.. image:: /images/tutorial_class/7.png

It is enough for now, our class with member is created.