Custom Form Handlers
====================

The :ref:`Platformus.Website <platformus-website>` extension offers the great :ref:`forms features <forms>`. You can describe your forms in the backend,
and then render them and get user feedback on any frontend view. When user fills the form and clicks the :guilabel:`Submit` button,
data is sent to a server and might be processed in any way you want. User input is handled by the implementations of the
`IFormHandler <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/FormHandlers/IFormHandler.cs#L18>`_ interface
which can return any ``IActionResult`` as the result.

The selected implementation receives the form object, all the user input (string values by field objects), and all the attachments
user has uploaded. Field values can be validated using the implementations of the
`IFieldValidator <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website/FieldValidators/IFieldValidator.cs#L15>`_
interface (you can use the
`ReCaptchaFieldValidator <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/FieldValidators/ReCaptchaFieldValidator.cs#L15>`_
as an example).

Platformus has the only one built-in implementation of the ``IFormHandler`` interface:
the `EmailFormHandler <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/FormHandlers/EmailFormHandler.cs#L18>`_ class.
It sends the user input to the specified email recipients.

Let’s implement our own form handler, which will just display the user input (but it could do anything else as well).
Create the ``DisplayUserInputFormHandler`` class inside the main web application project and implement the ``IFormHandler`` interface there:

.. code-block:: cs
    :emphasize-lines: 1

    public class DisplayUserInputFormHandler : IFormHandler
    {
      public IEnumerable<ParameterGroup> ParameterGroups => new ParameterGroup[] { };
      public string Description => "Our own form handler.";
	
      public async Task<IActionResult> HandleAsync(HttpContext httpContext, string origin, Form form, IDictionary<Field, string> valuesByFields, IDictionary<string, byte[]> attachmentsByFilenames)
      {
        StringBuilder body = new StringBuilder();

        foreach (KeyValuePair<Field, string> valueByField in valuesByFields)
          body.AppendFormat("<p>{0}: {1}</p>", valueByField.Key.Name.GetLocalizationValue(), valueByField.Value);

        return new ContentResult() { Content = body.ToString() };
      }
    }

Now, when our form handler class is added, navigate to the backend’s :guilabel:`Content/Forms` section and create or edit a form:

.. image:: /images/platformus_website/advanced/custom_form_handlers/1.png

Please note, that our new form handler C# class is automatically resolved and added to the drop down list. Click the :guilabel:`Save` button.

Now navigate to /en/contacts and fill out the form:

.. image:: /images/platformus_website/advanced/custom_form_handlers/2.png

Click the :guilabel:`Send` button. Output from our form handler is displayed:

.. image:: /images/platformus_website/advanced/custom_form_handlers/3.png

We could return some view, redirect, or any other action result we need.

Form Handler Parameters and Parameter Groups
--------------------------------------------

As well as the endpoints and data sources, form handlers support parameters and parameter groups. The implementation is absolutely the same,
so please just take a look at the :ref:`endpoints <custom-endpoints>` for the sample. Also, please take a look at the
`built-in form handler <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Website.Frontend/FormHandlers/EmailFormHandler.cs#L56>`_
to see how it gets the parameter value.