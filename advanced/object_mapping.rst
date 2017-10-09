Object Mapping
==============

Platformus has built-in object mapper that allows you to map the C# objects on the Platformus ones and vice versa.
Using this feature you can, for example,  create a comment object inside a
`custom form handler <http://docs.platformus.net/en/latest/advanced/custom_form_handler.html>`_.

Let’s see how it works. First of all, we need to create a class in the Platformus backend. Create a simple ``Cat`` class
with two properties: ``Name`` (localizable single line plain text) and ``Birthday`` (date):

.. image:: /images/advanced/object_mapping/1.png

It corresponds next  C# class (create it inside the main web application project):

.. code-block:: cs
    :emphasize-lines: 1

    public class Cat
    {
      public IDictionary<string, string> Name { get; set; }
      public DateTime Birthday { get; set; }
    }

Now you can use the
`StronglyTypedObjectMapper <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Domain/Mappings/StronglyTypedObjectMapper.cs#L15>`_ class
to work with the ``Cat`` objects. To select all the cats, use this code:

.. code-block:: cs
    :emphasize-lines: 1

    IEnumerable<Cat> cats = new StronglyTypedObjectMapper(this).All<Cat>();

To create a cat use the following code:

.. code-block:: cs
    :emphasize-lines: 5

    Cat cat = new Cat();

    cat.Name = new Dictionary<string, string>() { { "en", "Cat #1" }, { "ru", "Кот №1" }, { "uk", "Кіт №1" } };
    cat.Birthday = DateTime.Now;
	new StronglyTypedObjectMapper(this).Create(cat);