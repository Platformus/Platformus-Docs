Tutorial: Create Object
=======================

We are going to create an object. Please follow
`this tutorial <http://docs.platformus.net/en/latest/getting_started/tutorial_class.html>`_ to create
simple Platformus-based web application and class first. We will use it as a base.

Run your Platformus-based web application and go to the backend, then to the Objects list:

.. image:: /images/tutorial_object/1.png

As you can see, there is My Objects link in the Standalone section of the Objects list. And it is correct,
because we have created My Object standalone class on the
`previous step <http://docs.platformus.net/en/latest/getting_started/tutorial_class.html>`_. Now click
that link:

.. image:: /images/tutorial_object/2.png

There is empty list here, no objects are created.

Create Object
-------------

Click the Create my object link and fill the Create my object form as below:

.. image:: /images/tutorial_object/3.png

View Name Field
~~~~~~~~~~~~~~~

Using this field, you can override the default view name specified in the class. For example, you may
want to have some specific view for the home page and another view for all other pages, while their objects
have the same class Page. In this case, you can set Page as default view for the class Page and HomePage
as the view in the home page object.

URL Field
~~~~~~~~~

The URL of the object. This field is only displayed for the standalone objects, because embedded ones can’t
be accessed via URL. Culture code will be added to the URL of the object automatically.

My Property Field
~~~~~~~~~~~~~~~~~

We have added this property while creating the My Object class, so it is custom one. We will display value
of this field on the page later.

Now click the Save button. Our object is created:

.. image:: /images/tutorial_object/4.png

Open in the Browser
-------------------

Now let’s try to open our new object in the browser. Navigate to http://localhost:5000/en/my-object and…
we have error 500, because there is not view MyObject is created:

.. image:: /images/tutorial_object/5.png

Go to /Views/Default folder and copy file Page.cshtml as MyObject.cshtml and edit it as follows:

.. image:: /images/tutorial_object/6.png

Save it and refresh the browser:

.. image:: /images/tutorial_object/7.png

Our object is displayed correctly.