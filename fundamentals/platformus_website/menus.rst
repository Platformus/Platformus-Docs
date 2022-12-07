.. _menus:

Menus
=====

Menus are used for navigation on the frontend. You can manage them (create, edit, and delete) from the backend
using the :guilabel:`Content/Menus` section:

.. image:: /images/fundamentals/content/menus/1.png

Each menu item has localized name, URL, and position:

.. image:: /images/fundamentals/content/menus/2.png

:guilabel:`URL`
~~~~~~~~~~~~~~~~~~~~

``URL`` is where user is redirected when clicks the menu item.

:guilabel:`Position`
~~~~~~~~~~~~~~~~~~~~

``Position`` might be used to sort the menu items in the correct order.

Once menu is created, you can display it on the frontend using the built-in ``MenuViewComponent`` view component like this
(the menu code is passed as the parameter to identify the menu we want to display):

.. code-block:: html
    :emphasize-lines: 1

    @await Component.InvokeAsync("Menu", new { code = "Main", additionalCssClass = "master-detail__menu" })
	
Or using the view component tag helper:

.. code-block:: html
    :emphasize-lines: 1

    <vc:menu code="Main" additional-css-class="master-detail__menu" />

As you can see, an additional CSS class might be applied using the corresponding optional parameter.

The result can look something like this (note that the current menu item is highlighted):

.. image:: /images/fundamentals/content/menus/3.png

Menus are displayed using the built-in views
(`_Menu <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/Views/Shared/_Menu.cshtml>`_ and
`_MenuItem <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/Views/Shared/_MenuItem.cshtml>`_).
The HTML elements have unique CSS classes (the `BEM <https://getbem.com/>`_ methodology is used), so it is easy
to apply styles to them:

.. code-block:: html

    <div class="menu master-detail__menu">
      <div class="menu__items">
        <div class="menu__item menu__item--active">
          <a class="menu__item-name menu__item-name--active" href="/en/">Home</a>
        </div>
        <div class="menu__item">
          <a class="menu__item-name" href="/en/about-me">About me</a>
        </div>
        <div class="menu__item">
          <a class="menu__item-name" href="/en/contacts">Contacts</a>
        </div>
      </div>
    </div>

If you want to change the HTML, just copy these default views into your project and they will be used instead of the built-in ones,
so you will be able to modify them as you want.