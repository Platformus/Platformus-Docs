Cultures
========

Cultures are used to specify which languages (date formats and so on) your web application supports.
You can manage them (add, edit, and delete) from the backend using the :guilabel:`Administration/Cultures` section:

.. image:: /images/fundamentals/administration/cultures/1.png

Each culture has code and name. The :guilabel:`Is default` checkbox allows to specify whether this culture should be used
as the default one on the frontend (it means that this culture will be used when the culture is not implicitly selected).
And the :guilabel:`Is backend UI` specifies whether this cultured should be used as the backend one (UI localization and so on).

.. image:: /images/fundamentals/administration/cultures/2.png

You can see that there is the Neutral culture exists in the list. This culture is used to store the culture-neutral string values
using the `localizations <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Globalization.Data.Entities/Localization.cs#L12>`_.
When you describe your data model using the classes and members, you can specify, whether the particular string property
is localizable or not. If it is localizable, N editors will be displayed, one for each of the cultures. It looks like this:

.. image:: /images/fundamentals/administration/cultures/3.png

When your string property is not localizable, only the one editor will be displayed, and the property value will be saved
using the neutral culture.

By default, short culture code segment is used in the URL to specify which culture should be used for the request.
For example: /en/some-page. It is done in this way to make it possible for the pages to be indexed by the search engines
with the different cultures.  But if you are sure that your web application will always support the only one culture,
you can turn off this behavior using the
`configurations <http://docs.platformus.net/en/latest/fundamentals/administration/configurations.html>`_ and have shorter URLs.
In this case, the default culture will be used to display the content (but you can change the way culture is selected
for the requests).

There is the special
`DefaultCultureManager <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Globalization/CultureManager/DefaultCultureManager.cs#L14>`_
class that you can use to operate the cultures. It implements the
`ICultureManager <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Globalization/CultureManager/ICultureManager.cs#L9>`_
interface and it is registered as a service inside the DI, so you can replace it with your own implementation.