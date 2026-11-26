<!-- Fonte: JavaScript API Reference 24.2, aexjs/apex.item.html -->

# Namespace: item

## QuickNav

### Functions

* addAttachHandler
* create
* isItem

## apex.item

The apex.item namespace contains global functions related to Oracle APEX items.
The apex.item.create function defines the behavior for an item type.
The apex.item function provides access to an item interface for a specific item.

### Functions

#### (static) addAttachHandler(pHandler)

This function is only for item plug-in developers. It provides a way for item plug-ins to initialize
without having to render a call to a JavaScript function. The handler function is called when the page
initializes.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pHandler` | function | *pHandler( pContext$ )*. A function provided by the plug-in that will initialize all item instances of the plug-in type. The function receives a jQuery object that is the context in which the item(s) can be found. |

Since:
:   * 20.2

In this example the plug-in render function produces an input element with
class "mySuperInput". The following code goes in the plug-in's JavaScript file.

#### (static) create(pItemId, pItemImpl) → {object}

This function is only for item plug-in developers. It provides a plug-in specific implementation for the item.
This is necessary to seamlessly integrate a plug-in item type with the built-in item
related client-side functionality of Oracle APEX. A plug-in should call this method even if
it passes in an empty `pItemImpl` object. See also apex.item.addAttachHandler.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pItemId` | Element | string | The item name. This is also the id of the main DOM element associated with the item. For backward compatibility this can also be the main item DOM Element. Passing in an element is deprecated and the id/name should be used instead. |
| `pItemImpl` | object | function | An object with properties that provide any functions needed to customize the Oracle APEX item instance behavior. All the properties of this object are copied to the item interface so it is possible to add additional methods or properties to it. The item interface has default implementations for each of its methods that are appropriate for many page items particularly for items that use standard form elements. For each method of item you should check if the default handling is appropriate for your item plug-in. If it isn't you can provide your own implementation of the corresponding function through this `pItemImpl` object. The default behavior is used for any functions omitted. This parameter can also be a function that is called during creation with a single object argument that is the base item interface. The function should add any needed functions or properties to the item interface.  ItemImpl can contain any of the following properties: Properties  | Name | Type | Description | | --- | --- | --- | | `addValue` | function | *function(value, displayValue)* Specify a function for adding a value to the item, where the item supports multiple values. This is called by the item#addValue method which has no default behavior for adding a value. Currently there is no client-side functionality of Oracle APEX dependent on this. Note: Even if this function is defined, the default handling always calls the afterModify method. | | `afterModify` | function | *function()* Specify a function that is called after an item is modified. This is useful, for example as some frameworks need to be notified if widgets are modified, for example their value has been set, or they have been disabled in order to keep both the native and enhanced controls in sync. This callback provides the hook to do so. Note: This callback is deprecated. | | `delayLoading` | boolean | Specify if the item needs to delay APEX page loading. There are many places in the APEX framework where client-side logic is run after the page has finished loading, for example Dynamic Actions set to 'Fire on Initialization', or code defined in the page level attribute 'Execute when Page Loads'. If an item takes longer to initialize (for example if it uses a module loader like RequireJS to load additional modules, or if the underlying JavaScript widget itself takes longer to initialize), setting delayLoading to true allows you to tell APEX to wait for your item to finish initializing, before firing it's built in page load logic. This allows you as a developer to ensure that your item is compatible with these built-in APEX features like Dynamic Actions.  When this is set to true, *apex.item.create* will return a `jQuery` deferred object, which will need to be resolved in order for page loading to complete.  Note: If using this option, you must ensure your item initializes as quickly as possible, and also that the returned deferred object is always resolved, to avoid disrupting the default APEX page load behavior.  Note: It is not necessary for the plug-in item to provide the item#isReady or item#whenReady functions. They are added automatically. | | `disable` | function | *function()* Specify a function for disabling the item, which overrides the default item#disable behavior. The default behavior sets the disabled property of the item node to true. Providing this override could be useful for example where the item consists of compound elements which also need disabling, or if the item is based on a widget that already has its own disable method that you want to reuse. Ensuring the item can disable correctly means certain item related client-side functionality of Oracle APEX still works, for example when using the Disable action of a Dynamic Action to disable the item. Note: Even if this function is defined, the default handling always calls the afterModify method. | | `displayValueFor` | function | *function(value, [state]):string* Specify a function that returns a string display value that corresponds to the given value. This overrides the default behavior of the item#displayValueFor method. The default behavior supports a standard select element and conceals the value of password inputs. | | `enable` | function | *function()* Specify a function for enabling the item, which overrides the default item#enable behavior. The default behavior sets the disabled property of the item node to false. Providing this override could be useful for example where the item consists of compound elements which also need enabling, or if the item is based on a widget that already has its own enable method that you want to reuse. Ensuring the item can enable correctly means certain item related client-side functionality of Oracle APEX still works, for example when using the Enable action of a Dynamic Action to enable the item. Note: Even if this function is defined, the default handling always calls the afterModify method. | | `getValidationMessage` | function | *function():string* Specify a function to return the validation message, which overrides the default item#getValidationMessage behavior. This function is not needed if the item implementation uses the native HTML validation API such as `setCustomValidity`. | | `getValidity` | function | *function():ValidityState* Specify a function that returns a validity state object, which overrides the default item#getValidity behavior. The returned object must at a minimum have the Boolean valid property. It may include any of the properties defined for the HTML5 ValidityState object. The default implementation returns the validity object of the item element if there is one otherwise it returns { valid: true }. | | `getValue` | function | *function():string* Specify a function for getting the item's value, which overrides the default item#getValue behavior. The default behavior handles the standard HTML form elements. Ensuring the item returns its value correctly means certain item related client-side functionality of Oracle APEX still works, for example in Dynamic Actions to evaluate a When condition on the item, or when calling the JavaScript function $v to get the item's value. | | `hide` | function | *function()* Specify a function for hiding the item, which overrides the default item#hide behavior. This could be useful for example where the item consists of compound elements which also need hiding, or if the item is based on a widget that already has its own hide method that you want to reuse. Ensuring the item can hide correctly means certain item related client-side functionality of Application Express still works, for example when using the Hide action of a Dynamic Action, to hide the item. Note: if the item is in an element with an id that matches the name of the item with a '_CONTAINER' suffix then the container element is hidden and this function is not called. | | `isChanged` | function | *function():Boolean* Specify a function that returns true if the current value of the item has changed and false otherwise, which overrides the default item#isChanged behavior. This function allows the Warn on Unsaved Changes feature to work. The default implementation uses built-in functionality of HTML form elements to detect changes. If this function does not work correctly then changes to the plug-in item type value will not be detect and the user will not be warned when they leave the page. | | `isDisabled` | function | *function():Boolean* Specify a function that returns true if the item is disabled and false otherwise, which overrides the default item#isDisabled behavior. Ensuring the item returns its value correctly means certain item related client-side functionality of Oracle APEX still works, for example client-side validation and Interactive Grid. | | `item_type` | string | A string that identifies the type of the item. | | `getPopupSelector` | function | *function():string* Specify a function that returns a CSS selector that locates the popup used by the item. Any plug-in item type that uses a popup (a div added near the end of the document that is positioned near the input item and floating above it) needs to provide a CSS selector that locates the top level element of the popup. This allows the item type to be used in the Interactive Grid region or any other region that needs to coordinate focus with the popup. The default implementation returns null. In addition the top level popup element must be focusable (have attribute tabindex = -1).  For best behavior of a popup in the Interactive Grid. The popup should:  * have a way of taking focus * close on escape when it has focus * close when the element it is attached to loses focus * return focus to the element that opened the popup when it closes * manage its tab stops so they cycle in the popup or return to the element that opened the popup at the ends | | `loadingIndicator` | function | *function(loadingIndicator$):jQuery* Specify a function that normalizes how the item's loading indicator is displayed during a partial page refresh of the item. This function must pass the pLoadingIndicator$ parameter as the first parameter, which contains a jQuery object with a reference to the DOM element for the loading indicator. The function then adds this loading indicator to the appropriate DOM element on the page for the item, and also returns the jQuery object reference to the loading indicator, such that the framework has a reference to it, so it can remove it once the call is complete. This is used, for example, if the item is a Cascading LOV and the Cascading LOV Parent Item changes, or when setting the item's value by using one of the server-side Dynamic Actions such as Set Value - SQL Statement. | | `nullValue` | string | Specify a value to be used to determine if the item is null. This is used when the item supports definition of a List of Values, where a developer can define a Null Return Value for the item and where the default item handling needs to know this in order to assert if the item is null or empty. This can be done by following these steps: From the Render function in the plug-in definition, emit the value stored in p_item.lov_null_value as part of the item initialization JavaScript code that fires when the page loads. For example:  ```   # Assumes that you have some JavaScript function called 'com_your_company_your_item'   # that accepts 2 parameters, the first being the name of the item and the second being   # an object storing properties (say pOptions) required by the item's client side code.   apex_javascript.add_onload_code (       p_code => 'com_your_company_your_item('||           apex_javascript.add_value(               apex_plugin_util.page_item_names_to_jquery(p_item.name)||', {'||           apex_javascript.add_attribute(               'lovNullValue', p_item.lov_null_value, false, false)||      '});' ); ```  Then, in the implementation of com_your_company_your_item( pName, pOptions ) you have the value defined for the specific item's Null Return Value in the pOptions.lovNullValue property. This can then be used in your call to apex.item.create, to set the nullValue property.  Ensuring the nullValue property is set means certain item related client-side functionality of Oracle APEX still works, for example, in Dynamic Actions to correctly evaluate an is null or is not null when condition on the item, or when calling the JavaScript function item#isEmpty to determine if the item is null. | | `refresh` | function | *function()* Specify a function to refresh the item. This is called by the item#refresh method. The default behavior triggers event "apexrefresh" for legacy plug-in items. | | `reinit` | function | *function(value, display):function* Specify a function to initialize an item's value when it is reused in a new context. This is only called for column items every time a new record is being edited. The default behaviour calls item#setValue and suppresses the change event. Items that support cascading LOVs should implement this function to first set the item's value (which may also require adding the value as an option in the item), then return a function where the cascade will take place. | | `removeValue` | function | *function(value)* Specify a function for removing a value from the item, where the item supports multiple values. This is called by the item#removeValue method which has no default behavior for removing a value. Currently there is no client-side functionality of Oracle APEX dependent on this. Note: Even if this function is defined, the default handling always calls the afterModify method. | | `setFocusTo` | Element | string | function | Specify the element to receive focus when focus is set to the item using the item#setFocus method. This can be defined as either a jQuery selector, jQuery object or DOM Element which identifies the DOM element, or a no argument function that returns a jQuery object referencing the element. This can be useful when the item consists of compound elements, and you do not want focus to go to the element that has an ID matching the item name, which is the default behavior. Ensuring the item sets focus correctly means certain item related client-side functionality of Oracle APEX still works, for example when using the Set Focus action of a Dynamic Action to set focus to the item, when users follow the Go to Error link that displays in a validation error message to go straight to the associated item, or when the item is the first item on a page and the developer has the page level attribute Cursor Focus set to First item on page. | | `setStyleTo` | Element | string | function | Specify the element to receive style, when style is set to the item using the item#setStyle method. This can be defined as either a jQuery selector, jQuery object or DOM Element which identifies the DOM element(s), or a no argument function that returns a jQuery object referencing the element(s). This is useful when the item consists of compound elements, and you do not want style to be set to the element or just the element, that has an ID matching the item name which is the default behavior. Ensuring the item sets style correctly means certain item related client-side functionality of Oracle APEX still works, for example when using the Set Style action of a Dynamic Action to add style to the item.  Note: Even if this property is defined, the default behavior of item#setStyle calls the afterModify method. | | `setValue` | function | *function(value, displayValue, suppressChangeEvent)* Specify a function for setting the item's value, which overrides the default item#setValue behavior. The default behavior handles the standard HTML form elements. Ensuring the item can set its value correctly means certain item related client-side functionality of Oracle APEX still works, for example when using the Set Value action of a Dynamic Action to set the item's value, or when calling the JavaScript function $s to set the item's value. Note: Even when this function is defined, the default handling always calls the afterModify function and triggers the change event according to the pSuppressChangeEvent parameter. The pSuppressChangeEvent parameter is provided to this function for informational purpose only. In most cases it can be ignored. | | `show` | function | *function()* Specify a function for showing the item, which overrides the default item#show behavior. This is useful for example where the item consists of compound elements which also need showing, or if the item is based on a widget that already has its own show method that you want to reuse. Ensuring the item can show correctly means certain item related client-side functionality of Oracle APEX still works, for example when using the Show action of a Dynamic Action, to show the item. Note: if the item is in an element with an id that matches the name of the item with a '_CONTAINER' suffix then the container element is shown and this function is not called. | | `storageType` | string | A string that identifies how multiple values are stored and sent to the server. Only applies to items that support multiple values. This does not change how values are returned by item#getValue. Supported types are "separated" and "json-array". When `storageType` is "separated" then `separator` property is required. | | `separator` | string | A string that is used to separate multiple values. | |

Since:
:   * 5.1

##### Returns:

Returns a `jQuery` Deferred object when delayLoading is set
to true. The `jQuery` deferred object must be resolved in order for the
APEX page load to complete. If delayLoading is set to false (the default), then nothing is returned.

Type
:   object

The following example shows a call to apex.item.create( pNd, pItemImpl )
with most available callbacks and properties passed to illustrate the syntax (although
it is unlikely that any plug-in needs to supply all of these).

The following example shows a call to apex.item.create( pNd, pItemImpl )
with delayLoading option set to true. Doing so results in the create function returning a
deferred object, which must be later resolved in order for page load to complete.

The following example shows a call to apex.item.create where the
pItemImpl argument is a function. This item plug-in provides its own custom logic for
the setValue function. The plug-in supports multiple toolbar modes which can be set programmatically
with the custom function setToolbarMode.

#### (static) isItem(pItemId) → {boolean}

This function returns true if and only if there is a DOM element with id equal to pItemId that has had
an item interface created for it with apex.item.create.

For backward compatibility with items that don't call apex.item.create a default implementation
of item is used to treat any DOM element with an id as if it were an APEX item.
There are some simple items with only default behavior that can be used as an item even though isItem returns
false for it. This function allows you to distinguish items that explicitly create an
item interface from arbitrary DOM elements.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pItemId` | string | Item id. |

##### Returns:

true if there is an element with the given id that supports the item interface.

Type
:   boolean

The following will only hide the item if it is an APEX item.

Documentation generated by JSDoc 4.0.3 on Wed Nov 27 2024 04:42:15 GMT+0000 (Coordinated Universal Time)

Oracle APEX Release 24.2, JavaScript API Reference

Copyright © 2003, 2025, Oracle and/or its affiliates. All rights reserved.