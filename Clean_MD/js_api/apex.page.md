<!-- Fonte: JavaScript API Reference 24.2, aexjs/apex.page.html -->

# Namespace: page

## QuickNav

### Functions

* cancelWarnOnUnsavedChanges
* confirm
* isChanged
* submit
* validate
* warnOnUnsavedChanges

## apex.page

This namespace is used for all client-side page related functions of Oracle APEX.

### Functions

#### (static) cancelWarnOnUnsavedChanges()

Call to remove the handler that checks for unsaved changes. This is useful to do before any kind of cancel
operation where the user is intentionally choosing to lose the changes. It is not normally necessary to call
this function because the declarative attribute Warn on Unsaved Changes with value Do Not Check will do it
automatically. Adding the class `js-ignoreChange` to a link (anchor element)
or button will cause this function to be called before the link or button action.

The following sets up a handler on a custom cancel button, to leave the page without
checking for changes.

#### (static) confirm(pMessageopt, pOptionsopt)

Displays a confirmation dialog showing a message, pMessage, and depending on the user's choice, submits the page or
cancels submitting. Depending on the value of the page's Reload on Submit attribute, the page is submitted using
Ajax or with a normal form submission post request.

Once the user chooses to submit the page, the behavior is the same as for the apex.page.submit function.
The shorter alias for this function apex.confirm with the same parameters can also be used.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pMessage` | string | <optional> | The confirmation message to display. The default is "Would you like to perform this delete action?". It is best to supply your own message because the default message is not localized. Note: The default message is deprecated. In the future this argument will be required. |
| `pOptions` | string | Object | <optional> | If this is a string, it will be used to set the REQUEST value. If this is null or omitted, the page will be submitted with no REQUEST value. If this is an object, you can define the following properties:Properties  | Name | Type | Attributes | Description | | --- | --- | --- | --- | | `request` | string | <optional> | The REQUEST value. For the confirm function the default is "Delete". | | `set` | Object | <optional> | An object containing name/value pairs of items to set on the page prior to submission. The object properties are page item names and the item value is set to the property value. The default is to not set any page items. | | `showWait` | boolean | <optional> | If true, a 'Wait Indicator' spinner is displayed, which can be useful when running long page operations. The default is false. | | `submitIfEnter` | Event | <optional> | This option is not useful for the confirm function. | | `reloadOnSubmit` | string | <optional> | Override the reload on submit setting of the page. Set to one of the following: "A" (always) or "S" (success) | | `ignoreChange` | boolean | <optional> | If true (the default) and the warnOnUnsavedChanges feature is enabled, no warning will be given if there are changes. If false and the warnOnUnsavedChanges feature is enabled and there are changes, a warning will be given. If warnOnUnsavedChanges feature is disabled, there is never a warning. Set this to false if the submit will not actually save the data. | | `validate` | boolean | <optional> | If true, check the validity of page items and models before submitting the page. If anything is not valid then show an alert dialog and don't submit the page. The default is false. | |

Shows a confirmation dialog with the text 'Delete Department'.
If the user chooses to proceed with the delete, the current page
is submitted with a REQUEST value of 'DELETE'.

This example is the same as the previous one but uses the shorter alias.

This example shows a confirmation message with the 'Save Department?' text.
If the user chooses to proceed with the save, the page is submitted with a REQUEST value of 'SAVE' and 2 page
item values are set, P1_DEPTNO to 10 and P1_EMPNO to 5433.

This example is the same as the previous one but uses the shorter alias.

#### (static) isChanged() → {boolean}

Return true if any page items or APEX models on this page have changed since last being
sent to the server. Items that are disabled or are configured to ignore changes are not included in the check.
This will call the `pExtraIsChanged` function set in
apex.page.warnOnUnsavedChanges if one was supplied and only if no other changes are found first.

Tip: Put the page in debug mode to see debug info messages in the browser console reporting any changed models
or the first changed page item found.

See also item#isChanged, apex.model.anyChanges.

##### Returns:

true if there are any changes, otherwise false.

Type
:   boolean

The following example checks if the page is changed before performing some action.

#### (static) submit(pOptionsopt) → {boolean|undefined}

This function submits the page. The shorter alias for this function apex.submit with the same parameters
can also be used. Depending on the value of the page's Reload on Submit attribute, the page is submitted using
Ajax or with a normal form submission post request.

This function triggers a apex.event:apexbeforepagesubmit event on the apex.gPageContext$ which can be canceled
by an event handler. If canceled, the page is not submitted. Just before the page is submitted, this function
triggers a apex.event:apexpagesubmit event on the apex.gPageContext$, which cannot be canceled.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pOptions` | string | Object | <optional> | If this is a string, it will be used to set the REQUEST value. If this is null, the page will be submitted with no REQUEST value. If this is an object, you can define the following properties:Properties  | Name | Type | Attributes | Description | | --- | --- | --- | --- | | `request` | string | <optional> | The REQUEST value. For a submit function the default is null. | | `set` | Object | <optional> | An object containing name/value pairs of items to set on the page prior to submission. The object properties are page item names and the item value is set to the property value. The default is to not set any page items. | | `showWait` | boolean | <optional> | If true, a 'Wait Indicator' spinner is displayed, which can be useful when running long page operations. The wait indicator is created using apex.widget.waitPopup. The default is false. Note: When the page is submitted with ajax (controlled with the page attribute Reload on Submit = Only for Success) a progress spinner may still be shown as part of the ajax request even if showWait is false. | | `submitIfEnter` | Event | <optional> | If you only want to submit when the ENTER key has been pressed, call apex.page.submit in the keydown or keypress event handler and pass the event object in this parameter. | | `reloadOnSubmit` | string | <optional> | Override the reload on submit setting of the page. Set to one of the following: "A" (always) or "S" (success) | | `ignoreChange` | boolean | <optional> | If true (the default) and the warnOnUnsavedChanges feature is enabled, no warning will be given if there are changes. If false and the warnOnUnsavedChanges feature is enabled and there are changes there will be a warning. If warnOnUnsavedChanges feature is disabled there is never a warning. Set this to false if the submit will not actually save the data. | | `validate` | boolean | <optional> | If true, check the validity of page items and models before submitting the page. If anything is not valid then show an alert dialog and don't submit the page. The default is false. | |

##### Returns:

If the submitIfEnter option is specified, a Boolean value is returned.
If the ENTER key is not pressed, true is returned and if the ENTER key is pressed, false is returned.
If submitIfEnter is not specified, undefined is returned.

Type
:   boolean
    |
    undefined

Submits the current page with a REQUEST value of 'DELETE'.

This example is the same as the previous one but uses the shorter alias.

This example submits the page with a REQUEST value of 'DELETE' and two page item values are set,
P1_DEPTNO to 10 and P1_EMPNO to 5433 . During submit, a wait icon is displayed as a visual indicator for the user.

This example is the same as the previous one but uses the shorter alias.

This example shows how to submit the page when the ENTER key is pressed on a text input.

#### (static) validate(pLocationopt) → {boolean}

Check if any page items or submittable APEX models on the page are invalid.
Any errors are shown using the apex.message.showErrors function.

Note: This function does not actually perform any validation. Use HTML 5 validation attributes
or API to validate items.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pLocation` | string | Array.<string> | <optional> | Optional location of where to display messages. See apex.message.showErrors `location` option for details. Default is ["inline", "page"] |

##### Returns:

true if page is valid, otherwise false.

Type
:   boolean

The following example checks if the page is valid when a button with id checkButton is pressed.

#### (static) warnOnUnsavedChanges(pMessageopt, pExtraIsChangedopt)

Initialize a handler that checks for unsaved changes anytime the page is about to unload.
This is safe to call multiple times. The pMessage and pExtraIsChanged parameters override any previous values.
This function is called automatically when the page attribute Warn on Unsaved Changes is set to yes.
The main reason to call this manually is to customize the parameters.

The actual checking for changes is done by apex.page.isChanged.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pMessage` | string | <optional> | Message to display when there are unsaved changes. If the message is not given, a default message is used. Note: Most browsers do not show this message. |
| `pExtraIsChanged` | function | <optional> | Optional additional function to be called, checking if there are any unsaved changes. It should return true if there are unsaved changes, and false otherwise. It is only called if there are no changes to any models or page items. This is useful if there are non-standard state-full inputs on the page that are not APEX items and do not keep their state in an APEX model. It allows writing a custom function to detect if those non-standard inputs have changed. |

The following example enables the 'Warn on unsaved changes' feature with a custom message.

Documentation generated by JSDoc 4.0.3 on Wed Nov 27 2024 04:42:15 GMT+0000 (Coordinated Universal Time)

Oracle APEX Release 24.2, JavaScript API Reference

Copyright © 2003, 2025, Oracle and/or its affiliates. All rights reserved.