Backend Menu
============

All the backend (admin panel) menu groups and items come from the extensions. Each extension can provide one or more implementations of the
`IMetadata <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/IMetadata.cs#L9>`_ interface which allows to specify,
among other things, the menu items grouped by the menu groups. It is preferable to use the
`MetadataBase <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/MetadataBase.cs#L9>`_ class
to be able to override only the methods you want:

.. code-block:: cs
    :emphasize-lines: 6

    public class MyMetadata : MetadataBase
    {
      public override IEnumerable<MenuGroup> GetMenuGroups(HttpContext httpContext)
      {
        IStringLocalizer<Metadata> localizer = httpContext.GetStringLocalizer<Metadata>();

        return new MenuGroup[]
        {
          new MenuGroup(
            localizer["My Group"],
            1000,
            new MenuItem[]
            {
              new MenuItem("icon--icon1", "/backend/something-1", localizer["Something 1"], 1000, "ManageSomething1"),
              new MenuItem("icon--icon2", "/backend/something-2", localizer["Something 2"], 2000, "ManageSomething2"),
              new MenuItem("icon--icon3", "/backend/something-3", localizer["Something 3"], 3000, "ManageSomething3")
            }
          ),
        };
      }
    }

This file can be placed anywhere in the project, it will be resolved automatically by the
`default implementation <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/Providers/DefaultMenuGroupsProvider.cs#L18>`_ of the
`IMenuGroupsProvider <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/Providers/IMenuGroupsProvider.cs#L9>`_ inteface.

If the provided menu group’s name matches name of the existing one, the menu items of both will be merged in the single group according to the menu item positions.

Let’s look at the `MenuItem <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/MenuItem.cs#L8>`_ class’s properties.

``CssClass`` allows to specify the CSS class that will be added to the menu item HTML tag. Intended to provide a custom icon but can also be used to apply another styling.

``Url`` is the URL where user is navigates when clicks the menu item.

``Name`` will be displayed in the menu.

``Position`` is used to sort the menu items (and menu groups). Items with a lower position are placed higher.

``PermissionCodes`` contains an array of the codes of the :ref:`permissions <permissions>` which are required for user to have in order to see the menu item.