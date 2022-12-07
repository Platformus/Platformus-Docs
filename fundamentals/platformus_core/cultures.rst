Cultures
========

Cultures are used to specify which languages and data formats your web application supports.
You can manage them (create, edit, and delete) from the backend using the :guilabel:`Administration/Cultures` section:

.. image:: /images/fundamentals/administration/cultures/1.png

Each culture has two-letter language code, name, and other fields:

.. image:: /images/fundamentals/administration/cultures/2.png

:guilabel:`Two-letter language code`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This code complies with ISO 639-1. It is used, for example, as URL segment to determine request's language (see below).

:guilabel:`Is frontend default`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Specifies if this culture should be used as the default one on the frontend (it means that this culture will be used
when the culture is not explicitly provided).

:guilabel:`Is backend default`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Specifies if this cultured should be used as the backend (admin panel) one.

You can see that there is the Neutral culture exists in the list. This culture is used by the :ref:`Platformus.Website <platformus-website>`
extension to store the culture-neutral string values using the `localizations
<https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Data.Entities/Localization.cs#L12>`_.

When you create your own extension or describe your data model with classes and members using the :ref:`Platformus.Website <platformus-website>` one,
you can specify whether the particular string property is localizable or not. If it is localizable, N editors will be displayed,
one for each of the cultures. It looks like this:

.. image:: /images/fundamentals/administration/cultures/3.png

When your string property is not localizable, the only one editor will be displayed, and the property value will be saved
either using the localization with neutral culture (in case the :ref:`Platformus.Website <platformus-website>` extension is used)
or in the way you want it to be saved.

When using the :ref:`Platformus.Website <platformus-website>` extension, by default a short two-letter language code segment
is used in the URL on the frontend to specify which culture should be used for the request.
For example: /en/some-page. It is done in this way to make it possible for the pages to be indexed by the search engines
with the different languages.  But if you are sure that your web application will always support the only one language,
you can turn off this behavior using the :ref:`configurations <configurations>` and have shorter URLs.
In this case, the default culture will be used to display the content (but you can change the way culture is selected
for the requests; for example, the ``Accept-Language`` header can be used).

There is the special
`DefaultCultureManager <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core/Services/Defaults/DefaultCultureManager.cs#L15>`_
class that you can use to work with the cultures. It implements the
`ICultureManager <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core/Services/Abstractions/ICultureManager.cs#L13>`_
interface and it is registered as a service inside the DI, so you can replace it with your own implementation.