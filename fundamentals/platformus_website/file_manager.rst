.. _file-manager:

File Manager
============

File manager allows you to manage your files (upload and delete them) from the backend using the
:guilabel:`Content/File manager` section:

.. image:: /images/fundamentals/content/file_manager/1.png

Once a file is uploaded you can use it in different ways. You can copy a link to the file and paste it somewhere.
If it is an image, you can paste it in the HTML editor using the file selector (click the :guilabel:`Insert/edit image`
button and then the :guilabel:`Browse` one):

.. image:: /images/fundamentals/content/file_manager/2.png

Please note that if your class contains a member with the ``Image`` as the data type, you don’t need to upload an image
using the file manager manually. The image editor will upload, crop, and save the image for the object property automatically
(and the image path will be different: each object has its own images path that includes its identifier).