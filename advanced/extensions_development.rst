Extensions Development
======================

Platformus is based on the `ExtCore framework <http://extcore.net/>`_, so it is modular and extendable by default.
You can follow the `ExtCore documentation <http://docs.extcore.net/>`_ to understand better how everything works.

Platformus has the `Barebone extension <https://github.com/Platformus/Platformus/tree/master/src/Platformus.Barebone>`_,
which defines basic HTML layout, styles, scripts, standard tag helpers and so on. Each extension,
in order to have the unified look, must use the Barebone one.

Also, there is the Platformus.Infrastructure package, which defines shared classes which can be used
to add your menu items in the backend menu, to add your styles and scripts to the backend layout etc.