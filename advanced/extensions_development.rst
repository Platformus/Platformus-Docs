Extensions Development
======================

Platformus is based on the `ExtCore framework <https://extcore.net/>`_, so it is modular and extendable by default.
You can follow the `ExtCore documentation <https://docs.extcore.net/>`_ to understand better how everything works.

Platformus has the `Core extension <https://github.com/Platformus/Platformus/tree/master/src/Platformus.Core>`_,
which defines basic backend HTML layout, styles, scripts, standard tag helpers and so on. Each extension,
in order to have the unified backend UI look, must use the Core one.

Also, there is the Platformus.Core.Backend package, which defines shared classes which can be used
to add your menu items in the backend menu, to add your styles and scripts to the backend layout etc.