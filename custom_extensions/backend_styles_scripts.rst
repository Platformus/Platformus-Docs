Backend Styles and Scripts
==========================

When you develop a custom Platformus CMS extension you might need to add your own CSS styles and JavaScript scripts on the backend (admin panel) pages.
Same as for the :ref:`menu <backend-menu>`, it can be done by implementing the
`IMetadata <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/IMetadata.cs#L9>`_ interface or inheriting the
`MetadataBase <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/MetadataBase.cs#L9>`_ class.

Please, take a look at the `implementation <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata.cs#L14>`_
from the :ref:`Platformus.Core <custom-extension>` extension for a sample.

This file can be placed anywhere in the project, it will be resolved automatically by the
`default implementation <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/Providers/DefaultStyleSheetsProvider.cs#L15>`_ of the
`IStyleSheetsProvider <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/Providers/IStyleSheetsProvider.cs#L9>`_ interface and the
`default implementation <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/Providers/DefaultScriptsProvider.cs#L15>`_ of the
`IScriptsProvider <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata/Providers/IScriptsProvider.cs#L9>`_ interface.

It is preferable to use links to minified CSS and JavaScript files to save traffic and speed up page loading.
Also, you might need to :ref:`embed these files <embedded-resources>` into your extension to make it atomic.