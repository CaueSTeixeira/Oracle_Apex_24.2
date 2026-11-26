<!-- Fonte: JavaScript API Reference 24.2, aexjs/region.html -->

# Interface: region

## QuickNav

### Properties

* element
* filterRegionId
* parentRegionId
* type
* widgetName

### Methods

* alternateLoadingIndicator
* call
* focus
* off
* on
* refresh
* widget

## region

The region interface is used to access region related methods and properties. You get access
to the region interface for a region with the apex.region function.

Plug-in developers can define the behavior of their region by calling apex.region.create.

Since:
:   * 5.1

### Properties

#### element :jQuery

The jQuery object for the region element.

##### Type:

* jQuery

Get option element after initialization.

#### filterRegionId :string

For region plug-ins which support Faceted Search / Smart Filters it is possible to pass in the DOM ID of the
facetsRegion region in order for APEX to bind the two together. If provided, the region will be automatically refreshed as the filters change.
Further, if the region's refresh callback returns a Promise, APEX will also automatically perform the appropriate locking and unlocking
of the facetsRegion region during refresh.

##### Type:

* string

#### parentRegionId :string

Identifies the parent (master) region ID, if the region is the detail region of a master detail relationship.

##### Type:

* string

Get option parentRegionId after initialization.

#### type :string

Identifies the type of the region. Regions that don't implement a custom region interface have type "generic".

##### Type:

* string

Get option type after initialization.

#### widgetName :string

For regions that are implemented with a jQuery UI style widget, this is the name of the widget. For other
widget implementations it is null. It is used internally by the region#call, region#on and
region#off methods.

##### Type:

* string

Get option widgetName after initialization.

### Methods

#### alternateLoadingIndicator(pElement, pLoadingIndicator$) → {jQuery}

Return an alternative loading indicator for the given element. Not all regions have this method so
check if it exists before calling. For regions that support column items and when the column items may
not be visible on the screen at all times this allows the region to
place the loading indicator in an appropriate location. This can return the loading indicator passed in
or return a completely new loading indicator.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pElement` | Element | DOM element that may represent a column item. |
| `pLoadingIndicator$` | jQuery | A loading indicator that can be inserted in to the DOM where desired and returned or ignored. |

##### Returns:

loadingIndicator jQuery object or null if the region has no alternative for given element.

Type
:   jQuery

#### call(pMethod, …args) → {\*}

Calls a method on the widget associated with the region. This method only applies to
regions that are implemented with a jQuery UI style widget.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pMethod` | string |  | The string name of the widget method. |
| `args` | \* | <repeatable> | Any number of arguments to be passed to the widget method. |

##### Returns:

The return value depends on the method called.

Type
:   \*

The call method is a shorthand for calling methods on a widget. The following example
shows an Interactive Grid region with Static ID `emp` and two equivalent ways of invoking the
`getSelectedRecords` method.

#### focus()

Cause the region to take focus. Not all native or plug-in regions support taking focus. It is up to the
specific region to determine where focus will go. Some regions manage focus such that there is a single
tab stop (or limited number of tab stops) and they may put focus to where the user last had focus within
the region.

The default implementation sets focus to the first element in the region that is capable of being tabbed
to.

The following example will focus the region with Static ID "myRegion".

#### off(events, …args)

Removes an event handler from the widget element associated with this region. This method only applies to
regions that are implemented with a jQuery UI style widget. This means that region#widgetName
property must be defined and the region#widget method returns a value.

This is a shortcut for calling `apex.region(id).widget().off(...)`.
Unlike the jQuery object `off` method this does not return the
jQuery object and therefore is not chainable. See the jQuery documentation for details.

See also region#on.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `events` |  |  | One or more space-separated event types and optional namespaces as defined by the jQuery `off` method. For events defined by this region widget the event name prefix can be omitted. |
| `args` | \* | <repeatable> | Other arguments to be passed to the widget's jQuery object `off` method such as selector, data, and handler. |

This example removes all event handlers for the selectionChange event of an
Interactive Grid region. Note that the short event name "selectionChange" can be
used rather than the full name "interactivegridselectionchange".
See also interactiveGrid#event:selectionchange.

#### on(events, …args)

Attaches an event handler to the widget element associated with this region. This method only applies to
regions that are implemented with a jQuery UI style widget. This means that region#widgetName
property must be defined and the region#widget method returns a value.

This is a shortcut for calling `apex.region(id).widget().on(...)`.
Unlike the jQuery object `on` method this does not return the
jQuery object and therefore is not chainable. See the jQuery documentation for details.

See also region#off.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `events` |  |  | One or more space-separated event types and optional namespaces as defined by the jQuery `on` method. For events defined by this region widget the event name prefix can be omitted. |
| `args` | \* | <repeatable> | Other arguments to be passed to the widget's jQuery object `on` method such as selector, data, and handler. |

This example handles the selectionChange event of an Interactive Grid
region by logging a message to the console. Note that the short event name "selectionChange" can be
used rather than the full name "interactivegridselectionchange".
See also interactiveGrid#event:selectionchange

#### refresh(pKeepPagination) → {Promise}

Cause the region to get new data from the server or otherwise refresh itself. Not all regions support refresh.
Exactly what happens depends on the type of region.

This function should be used in place of the legacy way of refreshing a region, which was to trigger the
apexrefresh event on the region element.

The default implementation triggers the legacy apexrefresh event on the region element for backward compatibility
with old regions that don't implement this interface.

The refresh callback can and should return a Promise, in order for the caller to have more knowledge of its progress.
Whether it does return one depends on the region or plug-in.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pKeepPagination` | boolean | controls the pagination and scroll behavior after refresh. The exact behavior depends on the region. Not all regions support this parameter. For example Interactive Report will maintain the page and scroll offset. |

##### Returns:

Type
:   Promise

The following will refresh the region with Static ID "myRegion":

The following example will refresh an Interactive Report region while maintaining the same page.

#### widget() → {jQuery|null}

Returns the widget associated with the region or null if the region isn't implemented with a widget.
Some advanced region types such as Calendar, Interactive Grid, or Tree are implemented using a widget.
This function provides access to the widget typically by returning a jQuery object for the widget element.
You can then call widget methods on the jQuery object. See also the region#call method.

##### Returns:

jQuery object or null if there is no widget associated with the region.

Type
:   jQuery
    |
    null

The following adds a row to an Interactive Grid by using the region widget method to
access the interactiveGrid widget interactiveGrid#getActions method and then invoking the
`selection-add-row` action.

Documentation generated by JSDoc 4.0.3 on Wed Nov 27 2024 04:42:15 GMT+0000 (Coordinated Universal Time)

Oracle APEX Release 24.2, JavaScript API Reference

Copyright © 2003, 2025, Oracle and/or its affiliates. All rights reserved.