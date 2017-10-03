Tutorial: Basic Content Management
==================================

We have working Platformus-based web application. Let’s assume it is the default personal website
that goes with the installer. Now we are going to see how to add the blog section on that website.

First of all, we need the blog post pages, right? Each blog post post should have the same properties as the regular page,
but also it needs preview (the small piece of content), image, and creation date. In the Platformus context,
all the pages are objects which are described by the classes. Therefore, to create new type of page
(and new type of object) we need to create the corresponding class first.

Go and login to the backend (navigate to `http://localhost:5000/backend/ <http://localhost:5000/backend/>`_)
and then go to the Administration/Classes section. There are already two classes here: ``Page`` and ``Regular Page``.
The ``Page`` class is abstract, it means that it is used as the base class for the other ones (class copies all the members
of its parent class). Click the :guilabel:`Members` link of the ``Page`` class to see the list of its members.
As you can see, there are the standard page properties here, like ``URL``, ``Content``, ``Title``, ``META description``,
and ``META keywords``:

.. image:: /images/getting_started/tutorial_basic_content_management/1.png

Now return to the class list and click the :guilabel:`Create class` button. Select the ``Page`` class as the parent class
for our new one.  Fill the :guilabel:`Code`, :guilabel:`Name`, and :guilabel:`Pluralized name` fields as shown below:

.. image:: /images/getting_started/tutorial_basic_content_management/2.png

Click the :guilabel:`Save` button. New class is created. Now go to the list of its members. It is empty for now
(but don’t forget that our class will have all the members from the ``Page`` class, because it is selected
as the parent one). 

Let’s add the ``Preview`` member to our class. Click the :guilabel:`Create member` button and fill the :guilabel:`Code`,
:guilabel:`Name`, and :guilabel:`Position` fields as shown below:

.. image:: /images/getting_started/tutorial_basic_content_management/3.png

If we had a lot of the members, we could use tabs to group them on the object edit page, but in our case,
we only use it to group the properties that are related to SEO in the parent class. Position is set to 5,
because we want our property editor to appear before the ``Content`` property one
(``Content`` member has position set to 10).

Now click the :guilabel:`Property` tab and fill the fields as shown below:

.. image:: /images/getting_started/tutorial_basic_content_management/4.png

When you change the property data type, the set of the fields on this tab is changed too. You can add your own data types
and specify their properties (as well as the client-side editors that are used to edit them) in the
`Data types <http://docs.platformus.net/en/latest/fundamentals/administration/datatypes.html>`_ section.
For the properties that have short values we can set the :guilabel:`Is property visible in list` checkbox,
so that properties will be displayed in the object list (we will see that later).
Now click the :guilabel:`Save` button again, our member is created.

Add the ``Image`` and ``Creation date`` members in the same way (but select the ``Image`` and ``Date`` property types for them).
Our member list will look like this:

.. image:: /images/getting_started/tutorial_basic_content_management/5.png

That’s it, we are done with our data model for now. Let’s add some content. Go to the Content/Objects section.
Objects (and again, our pages are objects) are grouped by the parent classes (pluralized names are used to name the groups).
Objects of the classes that doesn’t have parent ones go under the Others group. Our ``Blog Post Page`` class is
already here:

.. image:: /images/getting_started/tutorial_basic_content_management/6.png

Click the :guilabel:`Create blog post page` button:

.. image:: /images/getting_started/tutorial_basic_content_management/7.png

As you can see, all the properties we have defined in the corresponding class are here. Fill the fields and click
the :guilabel:`Save` button. New blog post is created:

.. image:: /images/getting_started/tutorial_basic_content_management/8.png

There are only the properties are displayed whose members have :guilabel:`Is property visible in list` checkbox checked.

Now we have our blog post page object created. We can use different ways to present it (view, API, plain text and so on),
but now let’s use old good view for that.

Go to the Development/Views/Default section. The list of the views from the Default subdirectory is displayed (by default,
all the requests are handled by the ``DefaultController``, that’s why subdirectory has that name; you can change the way
requests are handled by Platformus, we will talk about that in the
`Advanced <http://docs.platformus.net/en/latest/advanced/index.html>`_ section):

.. image:: /images/getting_started/tutorial_basic_content_management/9.png

Click the :guilabel:`Create view` button and fill the fields as shown below:

.. image:: /images/getting_started/tutorial_basic_content_management/10.png

The HTML ifself is very simple. You can see that all the data comes from the view model. There is the ``Page`` property
which contains all the properties of our blog post page object that we have described by the class members
(and property names are the same as the member codes). This ``Page`` property is created for us by the corresponding data source.
If your view needs more different data in order to be rendered, just add more data sources that will provide this data
to the view model. Data sources are C# classes that implement the
`IDataSource <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/DataSources/IDataSource.cs#L10>`_
interface, you can `create your own ones <http://docs.platformus.net/en/latest/advanced/custom_data_sources.html>`_.
They can provide data in any way you need: to load some objects,
to take it from the web services (weather forecast?), or to return some hardcoded values. All the data sources
that are used to process the particular request are grouped inside the endpoint. Endpoints process the requests
and return response in Platformus-based web applications (as well as data sources, they are C# classes that implement the
`IEndpoint <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/Endpoints/IEndpoint.cs#L11>`_
interface, and you can `create your own implementations <http://docs.platformus.net/en/latest/advanced/custom_endpoints.html>`_).
We will see how this all works a bit later in this article. Now click the :guilabel:`Save` button. The view is created:

.. image:: /images/getting_started/tutorial_basic_content_management/11.png

We have described and created the content (our blog post page object), we have also created the presentation for that content
(our view). The last thing we must do to make it all work is to create the endpoint and the data source.
Go to the Development/Endpoints section. Click the :guilabel:`Create endpoint` button and fill the fields as shown below:

.. image:: /images/getting_started/tutorial_basic_content_management/12.png

Endpoints are very important. They define how your Platformus-based web application processes the HTTP requests.
By default, if there are no endpoints configured, you will have 404 response on every request. By specifying the URL template
for the endpoint, you tell the instance of the
`IEndpointResolver <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Routing/EndpointResolvers/IEndpointResolver.cs#L10>`_
interface which endpoint it should use to process the particular request (you can use {*url} one to handle all the requests).
It is done the similar way as the MVC routes configuration (endpoint is something like route and controller at once;
endpoints support URL parameters too). Also, you can specify which C# class (implementation of the ``IEndpoint`` interface)
will handle the request. You can write your own implementations of that interface and use them to handle the requests
(or you can take some third-party one and copy the DLL file with it to the Platformus extensions folder and use it).
Specify the view name that we have created earlier that will be used by this endpoint to render the response.
Click the :guilabel:`Save` button to create our new endpoint:

.. image:: /images/getting_started/tutorial_basic_content_management/13.png

One more thing about the endpoints. Default implementation of the ``IEndpointResolver`` interface checks endpoints,
sorted by the position, one by one (whether the current one’s URL template matches the request’s URL or not).
That’s why position field value is important. If you have a few endpoints that match the given URL, the first one will be used.

The last thing we have to do is to add the data source that will load the blog post page object by the value of the ``URL`` property
and assign it to the view model’s ``Page`` property (that will also be created). Click the :guilabel:`Data sources` link and then the
:guilabel:`Create data source` button. Fill all the fields as shown below and click the :guilabel:`Save` button:

.. image:: /images/getting_started/tutorial_basic_content_management/14.png

That’s it. Now we can test how our blog post page is displayed. Navigate to
`http://localhost:5000/en/blog/my-first-blog-post <http://localhost:5000/en/blog/my-first-blog-post>`_:

.. image:: /images/getting_started/tutorial_basic_content_management/15.png

It works! But we also need to have a page with all the blog posts. We will make it quickly, because now you know enough.
This page will display the blog posts, so we don’t need to create any new class (just create the regular page object with
the ``URL`` property value set to /blog). All we need is to create new view, endpoint and two data sources for it.
Let’s start from the view:

.. image:: /images/getting_started/tutorial_basic_content_management/16.png

As you can see, we will have a data source that will provide the ``BlogPosts`` view model property for us.
Also we have to create the _BlogPost partial view (inside the Shared folder):

.. image:: /images/getting_started/tutorial_basic_content_management/17.png

Now create the new endpoint (you have to have the separated endpoint for each page template (or view)):

.. image:: /images/getting_started/tutorial_basic_content_management/18.png

Because the page that will display the list of the blog posts is the page too, add the Page data source for
our new endpoint (the same way we have done that for the previous one). It will load our regular page object that holds
``Content`` and other properties of this page.

But in order to be able to display the blog posts on this page, we must add one more data source:

.. image:: /images/getting_started/tutorial_basic_content_management/19.png

As you can see, another C# class is selected for this data source. It provides more properties for us. For example,
it allows to specify the class of the objects to load, to specify which their relations (and relations of the relations and so on)
should be loaded, should we use filtering, sorting, or paging etc.

Everything is done. Now you can navigate to `http://localhost:5000/en/blog <http://localhost:5000/en/blog>`_
and see the result:

.. image:: /images/getting_started/tutorial_basic_content_management/20.png

Click the image to go to the blog post page. You can add the new menu item in the menu to have your blog there.

In the next tutorial we will see how to display comments on the blog post page and how to create them using the forms,
user input and `Platformus object mappers <http://docs.platformus.net/en/latest/advanced/object_mapping.html>`_.

