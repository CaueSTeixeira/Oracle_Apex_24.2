# 03_app_builder_dynamic_actions
Fonte: Oracle APEX 24.2 App Builder User's Guide — https://docs.oracle.com/en/database/oracle/apex/24.2/htmdb/

<!-- fonte: htmdb/managing-dynamic-actions.html -->
## Managing Dynamic Actions

Dynamic actions enable developers to define complex client-side behavior declaratively without the need for JavaScript.

* About Dynamic Actions
  Dynamic actions provide a way to define complex client-side behavior declaratively without the need for JavaScript. Using the Dynamic Action Create wizard, you specify an action that is performed when a defined set of conditions occur. You can also specify which elements are affected by the action, and when and how they are affected.
* About Dynamic Action Events
  You can define dynamic actions to fire based on events that happen on the page. Oracle APEX includes four different categories of events: Browser events, Framework events, Component events, and Custom events. This section describes all supported events, including the internal JavaScript event name in brackets.
* Creating a Dynamic Action
  Creating a dynamic action involves specifying when the action happens (with optional conditions), what action or actions are performed, and what elements are affected by the action. To learn more about any Property Editor attribute, select the attribute and click the Help tab in the central pane.
* Editing Dynamic Actions
  Once you create a dynamic action, you can modify attributes defined during the creation process, specify attributes not available during the process (such as specifying an Authorization Scheme) and add additional true actions.
* Defining Dynamic Action Event Scope
  After creating the dynamic action, the scope of the action can be modified to trigger only once, for the lifetime of the current page, or until triggering elements are updated by a Partial Page Refresh (PPR).
* Deleting a Dynamic Action
  Delete a dynamic action by selecting it in Page Designer and selecting Delete from the context menu.
* About Calling JavaScript Using a Dynamic Action
  You can execute JavaScript code by creating a dynamic action.
* Debugging Dynamic Actions
  Learn how to debug dynamic actions in APEX.

See Also:

Accessing Page Specific Utilities

### About Dynamic Actions

Dynamic actions provide a way to define complex client-side behavior declaratively without the need for JavaScript. Using the Dynamic Action Create wizard, you specify an action that is performed when a defined set of conditions occur. You can also specify which elements are affected by the action, and when and how they are affected.

Without any complex coding or knowledge of JavaScript, you can create
declaratively define how componentsrespond to various user
interactions such as button clicks, items changing, and so. An APEX dynamic actioin consists two parts:
**Triggers** and **Actions**. The Trigger
defines the condition upon which the Actions take place. Actions
enable you to dynamically do anything you would normally achieve using
a combination of JavaScript and CSS such as showing/hiding page
components, setting values, executing PL/SQL code and so on.

When working with dynamic actions, you should be mindful of the fact that the more
dynamic actions you add to a page, the greater your overall page size.
This is because the dynamic action framework emits additional code to
the client for each dynamic action defined, which then must be
downloaded and executed by the framework in the client.

The process of implementing a dynamic action involves the following steps:

1. Create (or use an existing) page component such as an item, button or region. This component is referenced within the dynamic action, in defining when it fires.
2. Create a dynamic action on the application page that invokes the action.
3. Run your application to test the dynamic action.

Tip:

See Debugging Dynamic Actions for information on how to debug problems.

Tip:

To view dynamic action examples, install the sample app, Sample Dynamic Actions. To learn more, see Installing Apps from the Gallery.

### About Dynamic Action Events

You can define dynamic actions to fire based on events that happen on the page. Oracle APEX includes four different categories of events: Browser events, Framework events, Component events, and Custom events. This section describes all supported events, including the internal JavaScript event name in brackets.

Browser Events

Note:

Refer to the W3C UI Events specification for
details about browser events or consult a reputable JavaScript reference. The events
that begin with `apex` are events that wrap native touch
events.

* Change (`change`) - Fires when a control loses the input focus and its value has been modified since gaining focus.
* Click (`click`) - Fires when the pointing device button is clicked over the triggering element.
* Double Click (`dblclick`) - Fires when the pointing device button is double clicked over the triggering element.
* Double Tap (`apexdoubletap`) - Fires when the pointer is doing a double tap/click.
* Get Focus (`focusin`) - Fires when the triggering element receives
  focus by either a pointing device or by tabbing into the element.
* Input (`input`) - This event is triggered every time the value of
  the element changes. It differs from the change event, which is only triggered
  when the value is committed, for example, by pressing the enter key or selecting
  a value from a list of options. Use the input event when you want to respond
  immediately to user input, whether it's typed using the keyboard or pasted from
  the clipboard.
* Key Down (`keydown`) - Fires when a key on the keyboard is pressed. Use this event when you want to capture special keystrokes such as arrow keys, after a key has been pressed.
* Key Press (`keypress`) - Fires when a key on the keyboard is pressed resulting in text being entered. Use this event when you want to capture actual text entry.
* Key Release (`keyup`) - Fires when a key on the keyboard is released. Use this event when you want to capture special keystrokes such as arrow keys, after a key has been released.
* Lose Focus (`focusout`) - Fires when the triggering element loses focus either by the pointing device or by tabbing out of the element.
* Mouse Button Press (`mousedown`) - Fires when the pointing device button is pressed over the triggering element.
* Mouse Button Release (`mouseup`) - Fires when the pointing device button is released over the triggering element.
* Mouse Enter (`mouseenter`) - Fires once when the pointing device is moved into the triggering element.
* Mouse Leave (`mouseleave`) - Fires once when the pointing device is moved away from the triggering element.
* Mouse Move (`mousemove`) - Fires when the pointing device is moved while it is over the triggering element.
* Pan (`apexpan`) - Fires when the pointer is down, then moved in a horizontal direction.
* Page Load - Fires when the page DOM content has loaded using the jQuery ready
  handler.
* Page Unload (`unload`) - Fires when a page is unloaded.
* Press (`apexpress`) - Fires when the pointer is down for greater than 250ms.
* Resize (`resize`) - Fires when the browser window is resized.
* Resource Load (`load`) - When the triggering element is the window element (using a JavaScript Expression value of `window` in the When attributes), the event fires when the browser finishes loading all content within a document, including window, frames, objects and images. For other elements, this event can only be used for elements associated with a URL: images, scripts, frames, iframes.
* Scroll (`scroll`) - Fires when a scrollable triggering element is scrolled. This could be the browser window (using a JavaScript Expression value of `window` in the When attributes), scrollable frames or elements with the `overflow` CSS property set to `scroll` (or `auto` when the element's explicit height is less than the height of its contents).
* Select (`select`) - Fires when a user selects some text in a text field.
* Swipe (`apexswipe`) - Fires when the pointer is moving fast in a horizontal direction.
* Tap (`apextap`) - Fires when the pointer is doing a small tap click.

Framework Events

* After Refresh (`apexafterrefresh`) - Fires after the triggering element has been refreshed. The event is only valid for triggering elements that perform Partial Page Refresh and fire this event. The native components that support this are Interactive Reports, Classic Reports, Charts, List View and all item types with cascading LOV support. Plug-ins might support this event as well. This event can be sent by the `apex.server.plugin` and `apex.server.process` APIs when the `refreshObject` option is provided. See apex.server in Oracle APEX API
  Reference
* Before Page Submit (`apexbeforepagesubmit`) - Fires before a page being submitted.
* Before Refresh (`apexbeforerefresh`) - Fires before the triggering element has been refreshed. The event is only valid for triggering elements that perform Partial Page Refresh and fire this event. The native components that support this are Interactive Reports, Classic Reports, Charts, List View and all item types with cascading LOV support. Plug-ins might support this event as well. This event can be sent by the `apex.server.plugin` and `apex.server.process` APIs when the refreshObject option is provided. See apex.server in Oracle APEX JavaScript
  API Reference.
* Dialog Closed (`apexafterclosedialog`) - Fires when an APEX dialog is closed. This event only fires when the dialog is closed using the 'Close Dialog' page process, or the 'Close Dialog' dynamic action.

Component Events

These events are available when there is a component (either an item, region, or dynamic action) available to your application that triggers a custom event. These events appear in the following format Event name [Component Name], for example the Change Order event triggered by the Shuttle native item type appears as Change Order [Shuttle]. Component events are either triggered from native components shipped with APEX, or from plug-in components you have installed into your application.

* Events triggered by native components:

  These will be in the format Event name [Component Name]. For help related to events raised by our native components, see `interactiveGrid` and `treeView`. See interactiveGrid and treeView in Oracle APEX JavaScript
  API Reference.
* Events triggered by plug-in components:

  These will be available when added to your current application and will be in the format Event name [Component Name]. For help related to events raised by plug-ins, refer to Help text on the plug-in configuration page, by navigating to Shared Components, Plug-ins, plug-in name, Help Text, where the plug-in author may have included documentation.

Custom Events

* Custom Events:

  By selecting Custom an additional field displays enabling you to
  define of a custom event. This is useful when the native or plug-in provided
  events are insufficient.

### Creating a Dynamic Action

Creating a dynamic action involves specifying when the action happens (with optional conditions), what action or actions are performed, and what elements are affected by the action. To learn more about any Property Editor attribute, select the attribute and click the Help tab in the central pane.

To create a dynamic action:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. Click the Dynamic Actions tab in the left pane.
3. Under Dynamic Actions, right-click Events and select Create Dynamic Action.

   Tip:

   You can also select an event type and then right-click to
   select Create Dynamic Action.

   The Property Editor displays Dynamic Action attributes.

   Page Designer indicates what actions are required next. If there
   is an error, a Messages icon displays next to the
   Save button. Click the
   Messages icon to view a dialog listing all the
   errors. Select an error to highlight the associated attribute in the
   Property Editor.
4. In the Property Editor, edit the following Dynamic Action attributes:

   Tip:

   To learn more about an attribute, select the attribute in the Property Editor and click the Help tab in the central pane.

   1. Identification, Name -
      Enter the name of the dynamic action.
   2. Execution , Sequence -
      Specify the sequence for this component. The sequence determines the
      order of execution.
   3. Execution , Event
      Scope - Select the scope of the event. Event Scope
      determines when the event is evaluated a second or successive time.
      Options include:

      * Static - Binds the event
        handler to the triggering element(s) for the lifetime of the
        current page, but is no longer bound if a triggering element
        is updated using Partial Page Refresh (PPR).
      * Dynamic - Binds the event
        handler to the triggering element(s) for the lifetime of the
        current page, irrespective of any triggering elements being
        recreated using Partial Page Refresh (PPR).
      * Once - Binds the event handler to the
        triggering element(s) only once. The dynamic action is not
        triggered again until after the page has been fully
        refeshed.
   4. Execution , Static
      Container (jQuery Selector) - Only displays if
      Event Scope is
      Dynamic. Enter the jQuery Selector of a
      static container for use by this dynamic action.

      You can improve the performance of dynamic actions that have an event
      scope of Dynamic. This must be an element on the page that itself
      does not get recreated, but contains the triggering elements that
      are recreated using Partial Page Refresh (PPR). This element
      reference needs to be defined as a jQuery selector.
   5. Execution , Type -
      Choose the type of execution method for the dynamic action. This
      defines if the actions are fired immediately, debounced, or
      throttled. Options include:

      * Immediate - Actions are
        executed immediately.
      * Debounce - Actions are
        only executed once after a specified time at the end of a
        single or series of events.

        Example 1: Update a text field if the user has
        stopped typing for 2 seconds and use the values last
        entered.

        Example 2: Refresh a region once after a click
        and ignore all other clicks in the next 5 seconds.
      * Throttle - Actions are
        executed at timed intervals when the action is fired
        multiple times.

        Example 1: During scrolling, update the current
        screen position at least every 2 seconds. The action will
        continue to fire if the user keeps scrolling.

        Example 2: As a user types, update a text field
        with the values entered at least every 2 seconds. The action
        will continue to fire as the user keeps typing.
   6. When, Event - Specify the event that causes the dynamic action to fire.
   7. When, Selection - Select the type of
      page element or construct to be used to trigger the event.

      Note:

      Only available if the
      event selected supports definition of a page element. Selecting any
      of the following events hides this attribute: Page Load, Page
      Unload, Resize, Before Page Submit, Orientation Change. All other
      event types show this field.
   8. Client-side Condition, Type - Optionally select the type of condition you want to control the true and false action processing of the dynamic action. If no client-side condition is defined, only true actions will fire. If a client-side condition is defined, the true action will fire when the condition is met, and the false action will fire when it is not.

      Note:

      Other properties will display conditionally based on the type, to declaratively allow you to define the condition. For example for the condition type `Item = Value`, you will see an `Item` and `Value` property, which will be checked in evaluating the condition.

   Next, define the action that to be performed if the event evaluates to True or False.
5. To edit an existing action:

   1. Expand the Dynamic Action tree and select an existing action (that is, select either True or False).
   2. In Property Editor, edit the following Action attributes:
      * Identification,
        Name - Enter the name of the action
        to help identify what the action does in Page Designer.
      * Identification,
        Action - Specify which action you
        want to perform.
      * Affected Elements, Selection Type-
        Select the page components to be affected when this action is
        executed. Additional options display depending upon the type of
        component selected.
      * Execution Options, Fire When Event Result Is - Specify whether this action fires when the triggering element condition is met by selecting True (True Action), or when it is not met by selecting False (False Action). If no condition is specified, only True actions fire.
      * Fire on Initialization - Specify if the action fires on initialization.

        Initialization has a slightly different meaning depending on how the dynamic action is defined. For dynamic actions defined to fire on interactive grid columns, this specifies if the action fires when the interactive grid row is activated for editing. For all other dynamic actions, this specifies if the action fires when the page loads.
6. To add a new action:

   1. Expand the Dynamic Action tree.
   2. Right-click the dynamic action and select either Create TRUE Action or Create FALSE Action.
   3. Edit the action in the Property Editor as described in the previous step.
7. Click Save.

See Also:

About Dynamic Action Events

### Editing Dynamic Actions

Once you create a dynamic action, you can modify attributes defined during the creation process, specify attributes not available during the process (such as specifying an Authorization Scheme) and add additional true actions.

To edit a dynamic action:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. Click the Dynamic Actions tab in the left pane. Dynamic actions are organized by events.
3. Expand the appropriate event and select the dynamic action.

   Attributes for the dynamic action display in the Property Editor.
4. In Property Editor, edit the appropriate Dynamic Action attributes.

   Tip:

   To learn more about an attribute, select the attribute in the Property Editor and click the Help tab in the central pane.
5. To edit an existing action:
   1. Expand the Dynamic Action tree to view the True or False nodes.
   2. Under True or False, select the action.
   3. Edit the action in the Property Editor.
6. To add a new action:
   1. Expand the Dynamic Action tree.
   2. Right-click the dynamic action and select either Create TRUE Action or Create FALSE Action.
   3. Edit the action in the Property Editor.
7. Click Save.

### Defining Dynamic Action Event Scope

After creating the dynamic action, the scope of the action can be modified to trigger only once, for the lifetime of the current page, or until triggering elements are updated by a Partial Page Refresh (PPR).

To specify event scope:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. Click the Dynamic Actions tab in the left pane.
3. Under Dynamic Actions, select the dynamic action.

   The Property Editor displays attributes for the dynamic action. Attributes are organized in groups.

   To find a group or attribute:

   * Search for the group or attribute - Enter
     keywords in the Filter Properties field. The Property Editor
     displays the group or attributes. To return to the default display,
     delete the keywords.
   * Use Go to Group - Click Go to
     Group and select the group. To return the default
     display, click Go to Group again and select
     Expand All.
4. Execution, Event Scope - Select
   the scope of the event, which determines when the event is evaluated a second or
   successive time. Options include:

   * Static - Binds the event handler
     to the triggering element(s) for the lifetime of the current page,
     but is no longer bound if a triggering element is updated using
     Partial Page Refresh (PPR).
   * Dynamic - Binds the event handler
     to the triggering element(s) for the lifetime of the current page,
     irrespective of any triggering elements being recreated using
     Partial Page Refresh (PPR).
   * Once - Binds the event handler to
     the triggering element(s) only once. The dynamic action is not
     triggered again until after the page has been fully refeshed.
5. Execution , Static Container (jQuery
   Selector) - Only displays if Sequence is
   Dynamic. Enter the jQuery Selector, of a static
   container, for use by this dynamic action.

   You can improve the performance of dynamic actions that have an
   event scope of Dynamic. This must be an element on the page that itself does
   not get recreated, but contains the triggering elements that are recreated
   using Partial Page Refresh (PPR). This element reference needs to be defined
   as a jQuery selector.
6. Execution , Type - Choose the
   type of execution method for the dynamic action. This defines if the actions are
   fired immediately, debounced, or throttled. Options include:

   * Immediate - Actions are executed
     immediately.
   * Debounce - Actions are only
     executed once after a specified time at the end of a single or
     series of events.

     Example 1: Update a text field if the user has stopped
     typing for 2 seconds and use the values last entered.

     Example 2: Refresh a region once after a click and ignore
     all other clicks in the next 5 seconds.
   * Throttle - Actions are executed
     at timed intervals when the action is fired multiple times.

     Example 1: During scrolling, update the current screen
     position at least every 2 seconds. The action will continue to fire
     if the user keeps scrolling.

     Example 2: As a user types, update a text field with the
     values entered at least every 2 seconds. The action will continue to
     fire as the user keeps typing.

   Note:

   If a Client-side Condition
   is defined, it will be evaluated when the dynamic action and itsActions are
   executed, not when the event fires.
7. Click Save.

### Deleting a Dynamic Action

Delete a dynamic action by selecting it in Page Designer and selecting Delete from the context menu.

To delete a dynamic action:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. Click the Dynamic Actions tab in the left pane.
3. Expand the appropriate event and locate the dynamic action to be deleted.
4. Right-click the dynamic action and select Delete.
5. Click Save.

### About Calling JavaScript Using a Dynamic Action

You can execute JavaScript code by creating a dynamic action.

You can also execute JavaScript code by creating a dynamic action with the
ActionExecute and Set Value. You can
also use JavaScript code for the condition of a dynamic action by setting the
Client-side Condition type to JavaScript Expression.

See Also:

Managing Dynamic Actions

### Debugging Dynamic Actions

Learn how to debug dynamic actions in APEX.

* About Debugging Dynamic Actions
  Learn about debugging dynamic actions.
* Debugging Dynamic Actions
  Debug an dynamic action by viewing the page in runtime and clicking Debug on the Runtime Developer toolbar.

#### About Debugging Dynamic Actions

Learn about debugging dynamic actions.

Debugging dynamic actions in APEX is slightly different than other debugging, because much of the processing done with the dynamic action framework is done on the client, not on the server. To debug dynamic actions, APEX outputs debug information to the browser's JavaScript console if your browser supports it (for example Firefox with Firebug installed shows the debug information in its Console pane). The debug information tells you when an action of a dynamic action fires, along with some additional information about the dynamic action, in the following format:

```sql
Dynamic Action Fired: [Dynamic Action name] ([Action name]) {JavaScript object containing all Dynamic Action information}
```

This format enables you to identify the dynamic action name, the action name which indicates which action is triggered, and the JavaScript object which contains a lot of information about the dynamic action, including the when element, the affected elements, the event object, and any data that may be associated with the dynamic action.

#### Debugging Dynamic Actions

Debug an dynamic action by viewing the page in runtime and clicking Debug on the
Runtime Developer toolbar.

To debug a dynamic action:

1. Ensure the application containing the dynamic action has Debugging enabled. See Utilizing Debug Mode.
2. Run the page containing the dynamic action.
3. Open the browser's JavaScript console.
4. From the Runtime Developer toolbar, find Debug.
5. On Runtime Developer toolbar, click Debug,
   Enable Debug. Use Enable Debug
   to specify the level of detail included when you click View Debug
   .

   Options include:

   * No Debug - Enables and disables
     Debug mode
   * Info (default) - The debug log
     contains the default or normal amount of information. This
     corresponds with a log level of 4 and a Debug URL argument of
     `YES`.
   * App Trace - The debug log
     contains messages up to level 6. This corresponds with a Debug URL
     argument of `LEVEL6`.
   * Full Trace - The log will contain
     the maximum amount of information. This corresponds with a Debug URL
     argument of `LEVEL9`. Full
     Trace can slow request processing but provides the
     most amount of detail.

   Since debug information is only output when running in Debug
   mode, leaving Debug mode switched on enables you to further test if dynamic
   actions are firing when you expect them to. For example if you have defined
   a dynamic action that fires when a certain item's value changes, change that
   item's value and the console shows the debug output if the dynamic action
   fires.
6. On Runtime Developer toolbar, click Debug,
   View Debug.

   Clicking View Debug  refreshes the page. If you have
   any dynamic actions that are set to fire on page load, you will see the
   debug output in the browser console.
