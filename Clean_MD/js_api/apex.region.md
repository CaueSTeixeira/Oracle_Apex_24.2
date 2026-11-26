<!-- Fonte: JavaScript API Reference 24.2, aexjs/apex.region.html -->

# Namespace: region

## QuickNav

### Functions

* create
* destroy
* findClosest
* isRegion

## apex.region

The apex.region namespace contains global functions related to Oracle APEX regions.
The apex.region function provides access to a region interface for a specific region.

Since:
:   * 5.1

### Functions

#### (static) create(pRegionId, pRegionImpl)

This function is only used by region plug-in developers. It provides a plug-in specific implementation for the region.

Use this function to give a region plug-in a set of behaviors defined by `pRegionImpl`.
The `pRegionImpl` parameter can provide its own implementation for standard
methods (such as refresh or focus) or omit them to get the default implementation.
It can add its own methods or properties as well.
It should include a `type` string property that specifies the type of region.

If the region is implemented with a jQuery UI style widget (using widget factory) then it should provide an
implementation for the region#widget method and define the region#widgetName property so that the
region#call method works. Note: jQuery UI is deprecated but the `call`
method and `widgetName` property remain for backward compatibility.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pRegionId` | string | Region id or region static id. This comes from the PL/SQL plug-in parameter `p_region.static_id`. |
| `pRegionImpl` | object | function | An object that provides the methods and properties for the region interface. All the properties of this object are copied to the region interface. It should provide a string `type` property. It can provide any additional methods that would be useful to developers. A default implementation is provided for any standard methods or properties omitted. See region for the properties and methods supported by the interface. This parameter can also be a function that is called during creation with a single object argument that is the base region interface. The function should add any needed functions or properties to the region interface. |

The following is region initialization code for a hypothetical region plug-in.
It provides implementations for the standard focus and refresh methods and adds a custom method
to filter the list.

The following example shows the same hypothetical region plug-in but using
the function callback for pRegionImpl.

#### (static) destroy(pRegionId)

This function is only for region plug-in developers. It will destroy and remove the behaviors associated with a
region element. It does not remove the region element from the DOM. It is not necessary to call this function
if the region will exist for the lifetime of the page. If the region is implemented by a widget that has a
destroy method then this function can be called when the widget is destroyed.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pRegionId` | string | Region id or region static id. It is a best practice to give a region a Static ID if it is going to be used from JavaScript otherwise an internally generated id is used. The region id is substituted in the region template using the #REGION_STATIC_ID# string. The region id can be found by viewing the page source in the browser. |

The following destroys the region interface but the region element remains on the page.

#### (static) findClosest(pTarget) → {region|null}

Returns the region that contains the `pTarget` element.
Returns null if there is no `pTarget` element or if it is
not in a region that has been initialized with a call to apex.region.create.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pTarget` | Element | string | A DOM element or CSS selector suitable as the first argument to the jQuery function. |

##### Returns:

A region interface or null if the element corresponding to
`pTarget` is not inside a region.

Type
:   region
    |
    null

The following will refresh the region that contains a button with class `refresh-button`
when it is clicked.

#### (static) isRegion(pRegionId) → {boolean}

This function returns true if and only if there is a DOM element with id equal to pRegionId that has had
a region interface created for it with apex.region.create.

To support older regions that
don't implement a region interface (by calling apex.region.create) the default implementation of
apex.region will attempt to treat any DOM element with an id as if it were an APEX region.
This function allows you to distinguish true APEX regions from arbitrary DOM elements.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pRegionId` | string | Region id or region static id. It is a best practice to give a region a Static ID if it is going to be used from JavaScript otherwise an internally generated id is used. The region id is substituted in the region template using the #REGION_STATIC_ID# string. The region id can be found by viewing the page source in the browser. |

##### Returns:

true if there is an element with the given id that supports the region interface.

Type
:   boolean

The following will only focus the region if it is an APEX region.

Documentation generated by JSDoc 4.0.3 on Wed Nov 27 2024 04:42:15 GMT+0000 (Coordinated Universal Time)

Oracle APEX Release 24.2, JavaScript API Reference

Copyright © 2003, 2025, Oracle and/or its affiliates. All rights reserved.