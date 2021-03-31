Extensions Development
======================

Platformus is based on the `ExtCore framework <https://extcore.net/>`_ and `Magicalizer <https://magicalizer.net/>`_,
so it is modular and extendable by default. You can follow the `ExtCore documentation <https://docs.extcore.net/>`_
to understand better how everything works.

While the `Platformus.Website <https://platformus.readthedocs.io/en/latest/extensions/platformus_website.html>`_
extension contains some frontend requests processing (the `WebsiteMiddleware
<https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/Middleware/WebsiteMiddleware.cs#L15>`_
can process requests using the `IEndpoint <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/Endpoints/IEndpoint.cs#L12>`_
interface implementations), your extensions still may contain standard things like controllers or pages. 

Basic backend UI (HTML, styles, scripts, tag helpers etc.) is defined inside the
`Platformus.Core.Backend <https://github.com/Platformus/Platformus/tree/master/src/Platformus.Core.Backend>`_
package of the `Platformus.Core <https://platformus.readthedocs.io/en/latest/extensions/platformus_core.html>`_ extension.
Using the `IMetadata <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Core.Backend/Metadata.cs#L11>`_
interface implementations you can replace existing styles and scripts, add new ones, add backend menu sections and items.