Tutorial: Basic Content Management
==================================

We have working Platformus-based web application. Let’s assume it is the default personal website
that goes with the installer. Now we are going to see how to add the blog section on that website.

First of all, we need the blog post page, right? Each post should have the same properties as the regular page,
but also it needs preview (the small piece of content), image, and creation date. In the Platformus context,
all the pages are objects which are described by the classes. Therefore, to create new type of page
(and new type of object) we need to create the corresponding class first.

Go and login to the backend (navigate to `http://localhost:5000/backend/ <http://localhost:5000/backend/>`_)
and then go to the Administration/Classes section. There are already two classes here: ``Page`` and ``Regular Page``.
The ``Page`` class is abstract, it means that it is used as the base class for the other ones (class copies all the members
of its parent class). Click the :guilabel:`Members` button of the ``Page`` class to see the list of its members.
As you can see, there are the standard page properties here, like ``URL``, ``Content``, ``Title``, ``META description``,
and ``META keywords``:

.. image:: /images/getting_started/tutorial_basic_content_management/1.png

Now return to the class list and click the :guilabel:`Create class` button. Select the Page class as the parent class
for our new one.  Fill the :guilabel:`Code`, :guilabel:`Name`, and :guilabel:`Pluralized name` fields as shown below:

.. image:: /images/getting_started/tutorial_basic_content_management/2.png

Click the :guilabel:`Save` button. New class is created. Now go to the list of its members. It is empty for now
(but don’t forget that our class will have all the members from the ``Page`` class because it is selected
as the parent one). 

Let’s add the ``Preview`` member to our class. Click the :guilabel:`Create member` button and fill the :guilabel:`Code`,
:guilabel:`Name`, and :guilabel:`Position` fields as shown below:

.. image:: /images/getting_started/tutorial_basic_content_management/3.png

If we had a lot of the members, we could use tabs to group them, but in our case, we only use it to group the
properties that are related to SEO in the parent class. Position is set to 5 because we want our property editor
to appear before the ``Content`` property one (``Content`` member has position set to 10).

Now click the :guilabel:`Property` tab and fill the fields as shown below:

.. image:: /images/getting_started/tutorial_basic_content_management/4.png

When you change the property data type, the set of the fields on this tab is changed too. You can add your own data types
and specify their properties (as well as the client-side editors that is used to edit them) in the
`Data types <http://docs.platformus.net/en/latest/fundamentals/administration/datatypes.html>`_ section.
For the properties that have short values we can set the :guilabel:`Is property visible in list` checkbox,
so that properties will be displayed in the object list (we will see that later).
Now click the :guilabel:`Save` button again, our member is created.

Add the ``Image`` and ``Creation date`` members in the same way (but select the ``Image`` and ``Date`` property types for them).
Our member list will look like this:

.. image:: /images/getting_started/tutorial_basic_content_management/5.png

That’s it, we are done with our data model for now. Let’s add some content. Go to the Content/Objects section.
Objects (and our pages are objects) are grouped by the parent classes (pluralized names are used to name the groups).
Objects of the classes that doesn’t have parent ones go under the Others group. Our ``Blog Post Page`` class is
already here:

.. image:: /images/getting_started/tutorial_basic_content_management/6.png

Click the :guilabel:`Create blog post page` button:

.. image:: /images/getting_started/tutorial_basic_content_management/7.png

As you can see, all the properties we have defined in the corresponding class are here. Fill the fields and click
the :guilabel:`Save` button. New blog post is created:

.. image:: /images/getting_started/tutorial_basic_content_management/8.png

There are only the properties is displayed which members have :guilabel:`Is property visible in list` checkbox checked.



Coming soon...