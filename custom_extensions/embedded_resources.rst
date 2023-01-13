.. _embedded-resources:

Embedded Resources
==================

Usually, your extension might need some resources (images, CSS, or JavaScript files etc.). You can add them to the host web application as regular static files,
but in most cases, you would like your extensions to be atomic, especially if they are distributed as NuGet packages. It can be done by defining the resources
that should be embedded in your *.csproj file:

.. code-block:: xml
    :emphasize-lines: 2

    <ItemGroup>
      <EmbeddedResource Include="wwwroot\**" />
    </ItemGroup>

After the resource is embedded, the underlying ExtCore framework will make it available using the HTTP requests. For example,
if you embed a file as /wwwroot/images/photo.jpg, it will be available as /wwwroot.images.photo.jpg.

Please look how the static files are `embedded <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Platformus.Core.Backend.csproj#L22>`_
and then `used <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Areas/Backend/Styles/checkbox.css#L27>`_
in the standard :ref:`Platformus.Core <platformus-core>` extension.