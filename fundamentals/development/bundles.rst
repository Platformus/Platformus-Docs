Bundles
=======

Bundles are used for automatic minification and concatenation of the CSS style and JavaScript script files.
When you create or edit a file and click the :guilabel:`Save` button, bundling process is automatically started
and minified and concatenated files are created according to the template you defined.
You can manage the bundles (add, edit, and delete) from the backend using the :guilabel:`Development/Bundles` section:

.. image:: /images/fundamentals/development/bundles/1.png

Bundle files use JSON format. There should be the only two properties in the root object: ``outputFile`` (string)
and ``inputFiles`` (string array):

.. image:: /images/fundamentals/development/bundles/2.png

The `RebuildAllBundles <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Designers/BundleManager.cs#L15>`_ method
of the `BandleManager <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Designers/BundleManager.cs#L13>`_ class
is used to build the bundles.