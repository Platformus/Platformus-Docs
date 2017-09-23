Installation
============

1. Download the latest Platformus archive from the `website <http://platformus.net/en/download>`_.
2. Extract it to a web server (as any other ASP.NET Core web application, Platformus can run using
the embedded Kestrel web server, or using the standalone web servers like
`Apache, Nginx, or IIS <https://docs.microsoft.com/en-us/aspnet/core/publishing/>`_.
3. Run Platformus using the following commands:

.. code-block:: bat
    :emphasize-lines: 1,2
    
    cd *path to the extracted archive*
	dotnet WebApplication.dll

As the result, you should see the following output:

.. image:: /images/getting_started/installation/1.png

4. Open your browser and navigate to `http://localhost:5000/ <http://localhost:5000/>`_.
5. As the result, you should see the Platformus installer:

.. image:: /images/getting_started/installation/2.png

Click the :guilabel:`Install now` button.

5. On the ``Usage Scenario`` page, select the scenario you want to be installed
(there will be more scenarios available in the future):

.. image:: /images/getting_started/installation/3.png

Scenario may include packages, storage scripts, view, scripts, styles and any other content.

Click the :guilabel:`Next` button.

6. On the ``Storage Type`` page, select the storage type you want to use:

.. image:: /images/getting_started/installation/4.png

Click the :guilabel:`Next` button.

7. On the ``Storage Connection`` page, type the connection string to connect your storage.
You can test the connection using the corresponding button:

.. image:: /images/getting_started/installation/5.png

Click the :guilabel:`Next` button.

8. On the ``Administrator Account`` page, type the username and password of the administrator account:

.. image:: /images/getting_started/installation/6.png

Click the :guilabel:`Next` button.

9. On the ``Language Packs`` page, select the languages you want to be available as the backend UI ones:

.. image:: /images/getting_started/installation/7.png

Click the :guilabel:`Next` button.

10. On the ``Finish`` page, you are ready to complete the installation:

.. image:: /images/getting_started/installation/8.png

Click the :guilabel:`Finish` button.

11. Installation completed successfully.

12. Now, please, restart your web application for the applied changes to take effect.
Don’t forget to remove the Platformus.Installer.dll file from the extensions folder.
Your web application for the selected usage scenario is ready to use:

.. image:: /images/getting_started/installation/9.png