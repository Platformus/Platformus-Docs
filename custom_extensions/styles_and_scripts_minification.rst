.. _styles-and-scripts-minification:

Styles and Scripts Minification
===============================

Good practice is to minimize number of the HTTP requests by combining the CSS and JavaScript files.
Also, these files can be minified to reduce their size by removing extra spaces, line breaks, replacing long variable names with the shorter ones etc.
(The JavaScript files could be also obfuscated, which makes reverse engineering much harder.)

By default, Platformus uses the `BundlerMinifier.Core <https://www.nuget.org/packages/BundlerMinifier.Core>`_ package for that.
To start using it add the corresponding reference to your *.csproj file:

.. code-block:: xml
    :emphasize-lines: 2

    <ItemGroup>
      <DotNetCliToolReference Include="BundlerMinifier.Core" Version="3.2.449" />
    </ItemGroup>

Now, add the following lines to the same project file to run the bundling and minification process automatically on build:

.. code-block:: xml
    :emphasize-lines: 1-3

    <Target Name="PrecompileScript" BeforeTargets="BeforeBuild">
      <Exec Command="dotnet bundle" />
    </Target>

Finally, the BundlerMinifier.Core package needs the bundleconfig.json file to be present in the project’s root folder:

.. code-block:: js
    :emphasize-lines: 2-22

    [
      {
        "outputFileName": "wwwroot/areas/backend/css/output.min.css",
        "inputFiles": [
          "Areas/Backend/Styles/input1.css",
          "Areas/Backend/Styles/input2.css",
          "Areas/Backend/Styles/input3.css"
        ]
      },
      {
        "outputFileName": "wwwroot/areas/backend/js/output.min.js",
        "inputFiles": [
          "Areas/Backend/Scripts/input1.js",
          "Areas/Backend/Scripts/input2.js",
          "Areas/Backend/Scripts/input3.js"
        ],
        "minify": {
          "enabled": true,
          "renameLocals": true
        },
        "sourceMap": false
      }
    ]

In this file you can specify which files and how exactly should be minified and combined.
You can use the `bundleconfig.json <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/bundleconfig.json>`_
file from the :ref:`Platformus.Core <platformus-core>` extension as a sample.