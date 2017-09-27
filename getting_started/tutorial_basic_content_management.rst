Tutorial: Basic Content Management
==================================

We have working Platformus-based web application. Let’s assume it is the default personal website
that goes with the installer. Now we are going to see how to add the blog section on that website.

First of all, we need the blog post page, right? Each post should have the same properties as the regular page,
but also it needs preview (the small piece of content), image and creation date. In the Platformus context,
all the pages are objects, which are described by the classes. Therefore, to create new type of page
(and new type of object) we need to create the corresponding class first.

Go and login to the backend (navigate to `http://localhost:5000/backend/ <http://localhost:5000/backend/>`_)
and then go to the Classes section. There are already two classes here: ``Page`` and ``Regular Page``.
The ``Page`` class is abstract, it means that it is used as the base class for the other ones (class copies all the members
of its parent class). Click the :guilabel:`Members` button of the ``Page`` class to see the list of its members.
As you can see, there are the standard page properties here, like URL, Title, and meta tags:

.. image:: /images/getting_started/tutorial_basic_content_management/1.png

Coming soon...