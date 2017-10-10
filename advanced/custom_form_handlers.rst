Custom Form Handlers
====================

Platformus.Forms extension offers the great forms features. You can describe your forms in the backend, and then render them
and get user feedback on any frontend view. When user fills the form and clicks the :guilabel:`Submit button`,
data is sent to a server and might be processed in any way you want. User input is handled by the implementations of the
`IFormHandler <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Forms/FormHandlers/IFormHandler.cs#L11>`_ interface.

The selected implementation gets the form object, all the user input (string values by field objects), and all the attachments
user has uploaded. It can return any ``IActionResult`` as the result.

Platformus has the only one built-in implementation of the ``IFormHandler`` interface:
the `EmailFormHandler <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Forms.Frontend/FormHandlers/EmailFormHandler.cs#L17>`_ class.
It sends the user input to the specified email recipients.

Let’s implement our own form handler, which will just display the user input. Create the ``DisplayUserInputFormHandler`` class inside the main web application project
and implement the ``IFormHandler`` interface there (in order to be able to write custom code in your Platformus-based web application, you can’t use Platformus
as the compiled executable; use it as the NuGet packages instead, or write your own extension project and then put its compiled DLL file inside the extensions folder):

.. code-block:: cs
    :emphasize-lines: 1

    public class DisplayUserInputFormHandler : FormHandlerBase
    {
      protected override IActionResult GetActionResult(IRequestHandler requestHandler, Form form, IDictionary<Field, string> valuesByFields, IDictionary<string, byte[]> attachmentsByFilenames)
      {
        StringBuilder body = new StringBuilder();

        foreach (KeyValuePair<Field, string> valueByField in valuesByFields)
          body.AppendFormat("<p>{0}: {1}</p>", requestHandler.GetLocalizationValue(valueByField.Key.NameId), valueByField.Value);

        return (requestHandler as Controller).Content(body.ToString());
      }
    }

As you can see, we used the `FormHandlerBase <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Forms/FormHandlers/FormHandlerBase.cs#L12>`_
abstract class instead of implementing the ``IFormHandler`` interface from scratch. It provides useful methods to manipulate the form handler parameters (see below).

Now, when our form handler class is added, navigate to the backend’s :guilabel:`Content/Forms` section and create or edit a form:

.. image:: /images/advanced/custom_form_handlers/1.png

Please note, that our new form handler C# class is automatically resolved and added to the drop down list. Click the :guilabel:`Save` button.

Now navigate to /en/contacts and fill out the form:

.. image:: /images/advanced/custom_form_handlers/2.png

Click the :guilabel:`Send` button. Output from our form handler is displayed:

.. image:: /images/advanced/custom_form_handlers/3.png

We could return some view, redirect, or any other action result we need.

Form Handler Parameters and Parameter Groups
--------------------------------------------

As well as the endpoints and data sources, form handlers support parameters and parameter groups. The implementation is absolutely the same,
so please just take a look at
the `one for the endpoints <http://docs.platformus.net/en/latest/advanced/custom_endpoints.html#endpoint-parameters-and-parameter-groups>`_.
Also, please take a look at the `built-in form handler <https://github.com/Platformus/Platformus/blob/master/src/Platformus.Forms.Frontend/FormHandlers/EmailFormHandler.cs#L17>`_
to see how it uses this feature.