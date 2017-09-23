Installation
============

1. Download the latest Platformus archive from the `website <http://platformus.net/en/download>`_.
2. Extract it to a web server (as any other ASP.NET Core web application, Platformus can run using
the embedded Kestrel web server, or using the standalone web servers like
`Apache, Nginx, or IIS <https://docs.microsoft.com/en-us/aspnet/core/publishing/>`_.
3. Run Platformus using the following commands:

.. code-block:: bat
    :emphasize-lines: 1,2
    
    :command:`cd` <path to the extracted archive>
	:command:`dotnet` WebApplication.dll

As the result, you should see the following output:

.. image:: /images/getting_started/installation/1.png

4. Open your browser and navigate to `http://localhost:5000/ <http://localhost:5000/>`_. As the result,
you should see the Platformus installer:

.. image:: /images/getting_started/installation/2.png

5. Click the :guilabel:`Install now` button.
6. Follow the installer.