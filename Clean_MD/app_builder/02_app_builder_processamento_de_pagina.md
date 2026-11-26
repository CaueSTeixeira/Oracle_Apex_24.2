# 02_app_builder_processamento_de_pagina
Fonte: Oracle APEX 24.2 App Builder User's Guide — https://docs.oracle.com/en/database/oracle/apex/24.2/htmdb/

<!-- fonte: htmdb/how-does-page-processing-and-page-rendering-work.html -->
## How Does Page Processing and Page Rendering Work?

Learn how the Oracle APEX engine renders and processes pages, when APEX issues implicit commits, how conditional rendering and processing works, and how to verify user identity or control access to controls and components.

* How the APEX Engine Renders and Processes Pages
  The Oracle APEX engine dynamically renders and processes pages based on data stored in Oracle database tables.
* About Implicit Commit Points
  Learn about when Oracle APEX issues implicit commits.
* Understanding Conditional Rendering and Processing
  Use conditions in an application to control how pages and page components display and when processes, computations, and validations execute.
* About Verifying User Identity
  Authentication is the process of establishing users' identities before they can access an application.
* About Controlling Access to Controls and Components
  Learn about controlling access to controls and components.

### How the APEX Engine Renders and Processes Pages

The Oracle APEX engine dynamically renders and processes pages based on data stored in Oracle database
tables.

To view a rendered version of your application, you request it from the APEX engine with a URL. When you run an application, the APEX engine relies on two processes:

* Show Page - Show Page is a page rendering process that assembles all the page attributes (including regions, items, and buttons) into a viewable HTML page. When you request a page using a URL, the engine is running Show Page.
* Accept Page - Accept Page performs forms page processing, including computations, validations, processes, and branching. When you submit a page, the APEX engine is running Accept Page or performing page processing during which it saves the submitted values in the session cache and then performs any computations, validations, or processes.

### About Implicit Commit Points

Learn about when Oracle APEX issues implicit commits.

Oracle APEX issues implicit commits at the following points:

* On load, after a page finishes rendering
* On submit, before branching to another page
* On submit, if one or more validations fail, before re-rendering the page
* After a computation
* After changing the value of an item, for example after a PL/SQL process that modifies a bind variable value or when `APEX_UTIL.SET_SESSION_STATE` is called.
* When `APEX_MAIL.PUSH_QUEUE` is called

See Also:

SET_SESSION_STATE Procedure and PUSH_QUEUE Procedure in Oracle APEX API
Reference

### Understanding Conditional Rendering and Processing

Use conditions in an application to control how pages and page components display and
when processes, computations, and validations execute.

A condition is a small unit of logic that helps you control the display
of regions, items, buttons, and tabs and the execution of processes, computations,
and validations. For example, when you apply a condition to a button, the rendering
engine evaluates the condition during the rendering (or Show Page) process. Whether
the condition passes or fails determines if the button displays.

You specify a condition by selecting a condition type. You can select a
condition type when you first create the control or component, or later when editing
the control or component.

Depending upon the type of condition you select, you enter the
appropriate values in the fields provided. The condition evaluates to true or false
based on the values you enter. Click the select list to view a complete list of all
available conditions for a given component or control.

See Also:

Available Conditions for a
detailed listing of available condition types

Example 3-1 Current Page is NOT in comma delimited
list

`Current Page is NOT in comma delimited list` evaluates to true if
the current page number is contained within the comma-delimited list of pages
provided. For example:

```sql
3,100,203
```

If the current page is 100, then this condition evaluates to true and
the condition passes.

Example 3-2 PLSQL Expression

Use `PLSQL Expression` to specify an expression in valid
PL/SQL syntax that evaluates to true or false. For example:

```sql
NVL(:MY_ITEM,'NO') = 'YES'
```

If the value of `:MY_ITEM` is YES, as in the previous
example, then the condition evaluates as true. If the value of :MY_ITEM is anything
other than YES, then the condition evaluates as false.

Example 3-3 Rows returned

`Rows returned`  expressed as a SQL query. If the query
returns one or more rows, then the condition evaluates as true. For example:

```sql
SELECT 1 FROM employees WHERE department_id = :P101_DEPTNO
```

This example references item `P101_DEPTNO` as a bind
variable. You can use bind variables within application processes and SQL query
regions to reference items from session state. If one or more employees are in the
department identified by the value of `P101_DEPTNO`, then the
condition evaluates as true.

See Also:

Referencing Session State Using Bind Variable Syntax

### About Verifying User Identity

Authentication is the process of establishing users' identities before they can
access an application.

Authentication may require a user to enter a user name and password, or may involve
the use of a digital certificate or a secure key.

Oracle APEX supports modular authentication, making it easy to switch authentication methods when needed. You can establish a user's identity by selecting from several built-in authentication methods, or by using a wizard to create your own custom authentication approach.

See Also:

Establishing User Identity Through Authentication

### About Controlling Access to Controls and Components

Learn about controlling access to controls and components.

While conditions control the rendering and processing of specific controls or components on a page, authorization schemes control user access. Authorization is a broad term for controlling access to resources based on user privileges.

Authorization schemes use the identities established by authentication to grant privileges on applications and objects within them. You can specify an authorization scheme for an entire application, a page, or a specific page control such as a region, item, or button. For example, you could use an authorization scheme to selectively determine which tabs, regions, or navigation bar entries a user sees.

See Also:

Providing Security Through Authorization

---

<!-- fonte: htmdb/managing-computations-validations-and-processes.html -->
## Managing Computations, Validations, and Processes

Enhance your application by including computations, validations, and processes.

**Computations** enable you to assign values to items.**Validations** are edit checks on specific items, pages, or columns. A **page process** performs an action at a specified point during the rendering or submission of the page. **Application processes** are blocks of PL/SQL logic that are set to run at specific points using processes from multiple pages of an application.

* Understanding Page Computations
  Use computations to assign a value to an identified item when a page is submitted or displayed.
* Understanding Validations
  Use validations to create edit checks on specific items, pages, or columns.
* Understanding Page Processes
  Create **page processes** to perform an action at a specified point during the rendering or submission of the page.
* Understanding Application Processes
  Create an application process to run a block of PL/SQL logic at a specific point from multiple pages of an application.
* About Branches
  A branch is an instruction to go to a specific page, procedure, or URL. For example, you can branch from page 1 to page 2 after page 1 is submitted. When you create a branch, you specify a Branch Point and Branch Type.
* Understanding Application Computations
  Create an application computation to set the value of a single page or application-level item. Application computations run at the same point across multiple pages in an application.
* Using the Attribute Dictionary
  Use the Manage Attribute Dictionary page to update values on the current page with those in the Attribute Dictionary, or to update the Attribute Dictionary with the values on the current page.

---

<!-- fonte: htmdb/creating-branches-validations-computations-and-processes.html -->
## Creating Branches, Validations, Computations, and Processes

Learn about managing branches, validations, computations, and processes in
Page Designer.

* Creating Pre-Rendering Branches, Computations, and Processes
  Create branches, computations, and processes that execute before rendering the page:
* Creating Page Submission Branches, Validations, Computations, and Processes
  Create page submission branches, validations, computations, and processes in the Processing tab.

See Also:

* Managing Computations, Validations, and Processes
* Controlling Navigation Using Branches

### Creating Pre-Rendering Branches, Computations, and Processes

Create branches, computations, and processes that execute before rendering the
page:

To create branches, computations, and processes that execute before
rendering the page:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In the left pane, select the Rendering tab.
3. Expand the Pre-Rending node at the top of the Rendering tab.
4. Determine the processing point. Right-click Before Header, After Header, or Before Regions to display the context menu for that processing point.
5. Select the appropriate option: Create Branch, Create Computation,
   or Create Process.
6. Edit the appropriate attributes in the Property Editor.

   Tip:

   To view help for an attribute, select the attribute in the Property Editor and click the Help tab in the central pane.
7. Click Save or Save and Run Page.

Tip:

If you have changed the default display to group components by component type, then you must to navigate to the Processing tab to maintain pre-rendering components.

See Also:

Managing Computations, Validations, and Processes

### Creating Page Submission Branches, Validations, Computations, and Processes

Create page submission branches, validations, computations, and processes in the
Processing tab.

To create branches, validations, computations, and processes that execute
when the page is submitted:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In the left pane, select the Processing tab.
3. Navigate to After Submit, Validating, Processing, or After Processing as appropriate within the processing tree.
4. Right-click the identifier or an existing component to display the context menu for that processing point.
5. Select Create Branch, Create Validation, Create Computation, or Create Process.
6. Edit the appropriate attributes in the Property Editor.

   Tip:

   To view help for an attribute, select the attribute in the Property Editor and click the Help tab in the central pane.
7. Click Save or Save and Run Page.

Tip:

You can use context menus to duplicate, delete, and copy a component to other pages.

See Also:

Managing Computations, Validations, and Processes

---

<!-- fonte: htmdb/understanding-page-processes.html -->
## Understanding Page Processes

Create **page processes** to perform an action at a specified point during the rendering or submission of the page.

* About Page Processes
  A page process performs an action at a specified point during the rendering or submission of the page.
* Creating Page Processes
  Create a page process in Page Designer.
* Editing Page Processes
  Learn about editing page process attributes in Page Designer.
* Understanding Background Page Processing
  Background page processing enables developers to run a sequence of page processes that can execute in the foreground or in the background.

---

<!-- fonte: htmdb/about-page-processes.html -->
## About Page Processes

A page process performs an action at a specified point during the rendering or
submission of the page.

For example, you can create a page process to execute logic or to make a call to the APEX engine. A page process is a unit of logic that runs when a specific event occurs, such as loading or submitting a page.

From a functional perspective, there is no difference between page-level and application-level processes. The difference between these two process types is where the process is defined, that is at the page-level or at the application level.

You create a page process in Page Designer. In either the Rendering or Processing tab,
locate the node where the process will occur, right-click, and select Create
Process. The process Type determines what attributes you need to
configure.

Supported Process Types

Note:

Depending on your application configuration, you may also have additional process
type plug-ins. These display as <My Plug-in> [Plug-in].

Supported page process Types include:

* Clear Session State - Process to clear session state
  stored within Oracle APEX.
* Close Dialog - Process to close the current modal or
  non-modal dialog page.
* Data Loading - Process to load data into the target table
  or collection based on the given data load definition.
* Download - Downloads one or multiple files. This process
  type works in Before Header position at Page Rendering or in Page Processing
  when submitting a page. The processing stops after this process is
  executed.
* Execute Code - Process to execute PL/SQL code.
* Execution Chain - Execute a sequence of page
  processes, either in the foreground or in the background..
* Form - Automatic Row Processing (DML) - Process to
  insert, update, or delete a form region row(s).
* Form - Initialization - Process to initialize form region
  items. Initialization can either be fetching data from the region source, using
  the primary key value(s) or simple initialization of the form region items.
  Human Task - Create - Process to create a human task, using an existing task
  definition from the application.
* Human Task - Create - Process to create a
  human task, using an existing task definition from the application.
* Human Task - Manage - Process to manage a human task. The
  different types of task management are Approve, Reject, Claim, Release,
  Delegate, Forward, Cancel, Comment and Invite Participant.
* Interactive Grid - Automatic Row Processing (DML) -
  Process to insert, update, or delete Interactive Grid rows.
* Invoke API - Process to invoke a procedure
  or function stored in the local database, or an operation defined in a REST Data
  Source.
* Print Report - Process to print a report using a report query.
* Reset Pagination - Process to reset pagination of reports
  on the current page.
* Send E-Mail - Process to send an email, and optionally
  one or more attachments, from the application.
* Send Push Notification - Sends a push
  notification to a user. All devices that the user subscribed to will receive the
  push notification.
* Server Side Geocoding - Only supported on Oracle
  Autonomous Database.

  This process type provides Geocoding (turning a postal address
  to a coordinate) functionality. Geocoding is performed by calling
  `SDO_GCDR.ELOC_GEOCODE`, which does a REST request to the
  Oracle Elocation Geocoding Service (elocation.oracle.com). For further
  information on this function, see SDO_GCDR.ELOC_GEOCODE
  in Oracle Spatial Developer's
  Guide.

  Geocoding input data comes from page items, which are mapped to address parts
  like Street, House Number, Postal Code or City. The process populates a
  coordinate and match vector page item with the results of the first matched
  address. In addition, all matches can be loaded into a collection for
  further processing. If Sanitize Address is enabled,
  address part page items will be overwritten with the sanitized values of the
  first matched address.
* User Preferences - Process to set User Preferences for
  the end user.
* Web Service - Process to consume the specified Web
  service.
* Work Flow - Process to perform the following
  operations on a Workflow:
  + Start a new Workflow Instance based on the selected
    Workflow Definition.
  + Terminate, Suspend, Resume or Retry an existing Workflow
    Instance.

  See About Using Workflows in Page Processes.

See Also:

* Understanding Application Processes
* Accessing Page Specific Utilities

---

<!-- fonte: htmdb/creating-a-page-processes.html -->
## Creating Page Processes

Create a page process in Page Designer.

To create a page process:

1. View the page in Page Designer.
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

      Page Designer appears.
2. In either the Rendering or Processing tab, locate the node where the process will occur. Right-click and select Create Process.
3. Page Designer indicates what to do next. If there is an error, the Show
   Messages icon displays in the Page Developer toolbar.
   1. Click the Show Messages icon on the Page
      Designer toolbar.

      The Messages dialog displays errors that must be
      addressed.
   2. Select an error to highlight the associated attribute in the Property
      Editor.

      To learn more about an attribute, select the attribute in the
      Property Editor and click the Help tab in the central pane.
4. Identification, Name - Enter the name of the process for easy identification by
   developers.
5. Identification, Type - Specify which process type to execute. The Type you
   select determines what attributes display next.

   Consider the following examples.

   * If Identification, Type is Execute
     Code:
     + Identification, Type - Select Execute
       Code.
     + Source, Location - Select where the process
       executes. Select either Local Database or
       REST Enabled SQL.
     + Source, Language - Select the language used to
       execute the entered code.
     + Source, PL/SQL - Enter the PL/SQL code to be
       executed.
   * If Identification, Type is Invoke
     API:
     + Identification, Type - Select Invoke
       API.
     + Settings, Type - Select what process executes.
       Options include: PL/SQL Package,
       PL/SQL Procedure or Function, or
       REST Source.

       What
       displays next, depends upon the Settings, Type you select.
       Consider the following examples:

       If
       Settings, Type is PL/SQL Package:
       - Settings, Type - Select PL/SQL
         Package.
       - Settings, Package - Enter the
         case-sensitive PL/SQL package name. You can type in
         the name or pick from the list.
       - Settings, Procedure or Function - Enter
         the case-sensitive procedure or function name
         defined in the selected PL/SQL package. You can type
         in the name or pick from the list.

       If Settings, Type is
       PL/SQL Procedure or Function:
       - Settings, Type - Select PL/SQL Procedure
         or Function.
       - Settings, Procedure or Function - Enter
         the case-sensitive procedure or function name
         defined in the selected PL/SQL package. You can type
         in the name or pick from the list.

       If Settings, Type is
       REST Source:

       - Settings, Type - Select REST
         Source.
       - Settings, REST Source - Select the REST
         Source which contains the Operation to be invoked.
       - Settings, Operation - Select the Operation
         to invoke. The select list shows the name, if configured
         for the REST Operation. Otherwise, its HTTP method and
         URL pattern will be shown.
6. Under Execution :
   1. Execution, Sequence - Specify the sequence for this computation. The
      sequence determines the order of execution.

      If two components have the same sequence value, then
      they may be executed in a different order when the application is
      exported and imported into another environment.
   2. Execution, Point - Select the point at which this process is
      executed.
   3. Execution, Run Process - Select the frequency that this process
      executes.
7. Under Success Message:
   * Success Message, Success Message - Enter the success message for this
     process.

     If the process runs and does not generate an error, then this
     process success message displays in the notification section of the
     resulting page displayed. If you are branching to another page using a
     URL redirect, you may need to check the preserve success
     message attribute.

     To learn more, select the
     attribute in the Property Editor and click the Help tab in the central
     pane.
8. Under Error:
   1. Error, Error Message - Enter the error message for this process.

      This message displays if an unhandled exception is
      raised. After any error processing stops, a rollback is issued and
      an error message displays.
   2. Error, Display Location - Select where this process error message
      displays, when the process fails to complete successfully.

      Option include:

      * Inline in Notification - The
        process error message displays in the Notification area (defined
        as part of the page template).
      * On Error Page - Error
        displays on a separate error page.
9. Click Save.

See Also:

* Creating Pre-Rendering Branches, Computations, and Processes
* Creating Page Submission Branches, Validations, Computations, and Processes

---

<!-- fonte: htmdb/editing-page-processes.html -->
## Editing Page Processes

Learn about editing page process attributes in Page Designer.

* Editing Page Process Attributes
  Edit a page process in Page Designer.
* Controlling When a Page Process Executes
  Control when a process executes by editing the Sequence and Point attributes.
* Making a Page Process Conditional
  Create a conditional page process by editing Server-side Condition attributes.
* Creating Page Process Success and Error Messages
  Define both success and error messages that display when a process runs.

### Editing Page Process Attributes

Edit a page process in Page Designer.

To edit an existing page process:

1. View the page in Page Designer.
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

      Page Designer appears.
2. Click the Processing tab in the left pane.
3. In either the Rendering or Processing tab, expand the nodes to locate and select the process.

   Process attributes display in the Property Editor. Attributes are organized in groups.

   To find a group or attribute, enter keywords in the Filter Properties field.
   The Property Editor displays the group or attributes. Or, you can click
   Go to Group and select the group.
4. Edit the appropriate attributes:

   Tip:

   To learn more about an attribute, select the attribute in the Property Editor and click the Help tab in the central pane.
5. Click Save.

### Controlling When a Page Process Executes

Control when a process executes by editing the Sequence and Point
attributes.

To control when a process executes, edit the Sequence and Point
attributes:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. Click the Processing tab in the left pane.
3. In either the Rendering or Processing tab, expand the nodes to locate and
   select the process.

   Process attributes display in the Property Editor. Attributes are
   organized in groups.
4. Under Execution :
   1. Execution, Sequence - Specify the sequence for this computation. The
      sequence determines the order of execution.

      If two components have the same sequence value, then
      they may be executed in a different order when the application is
      exported and imported into another environment.
   2. Execution, Point - Select the point at which this process is
      executed.
   3. Execution, Run Process - Select the frequency that this process
      executes.
5. Click Save.

See Also:

Editing Page Process Attributes

### Making a Page Process Conditional

Create a conditional page process by editing Server-side Condition
attributes.

To create a conditional page process:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. Click the Processing tab in the left pane.
3. In either the Rendering or Processing tab, expand the nodes to locate and
   select the process.

   Process attributes display in the Property Editor. Attributes are
   organized in groups.
4. Under Server-side Condition:
   1. Server-side Condition, When Button Pressed - If you want this page
      processing component to execute only when the specified button is
      clicked, select a button from the list. You can incorporate this button
      condition with other conditions to further refine when this page
      processing component executes.
   2. Server-side Condition, Execution Type - Select a condition type that
      must be met in order for this component to be rendered or
      processed:

      To learn more, select the attribute in the Property Editor and click
      the Help tab in the central pane.
5. Click Save.

### Creating Page Process Success and Error Messages

Define both success and error messages that display when a process runs.

You can define both success and error messages that display when a process runs.
How an error message displays depends upon the processing point. For processes with a
processing point of `On Submit - Before Computation and Validations` or
`On Submit - After Computations and Validations`, you can specify
whether the error message displays inline on the current page (the default) or on a
separate page. For all other page processes, error messages display on a separate error
page.

To create a page process error or success message:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. Click the Processing tab in the left pane.
3. In either the Rendering or Processing tab, expand the nodes to locate and
   select the process.

   Process attributes display in the Property Editor. Attributes are
   organized in groups.
4. Under Success Message:
   * Success Message, Success Message - Enter the success message for this
     process.

     If the process runs and does not generate an error, then this
     process success message displays in the notification section of the
     resulting page displayed. If you are branching to another page using a
     URL redirect, you may need to check the preserve success
     message attribute.

     To learn more, select the
     attribute and click the Help tab in the central pane.
5. Under Error:
   1. Error, Error Message - Enter the error message for this process. This
      message displays if an unhandled exception is raised. After any error
      processing stops, a rollback is issued and an error message
      displays.
   2. Error, Display Location - Select where this process error message
      displays, when the process fails to complete successfully.

      Option include:

      * Inline in Notification - The
        process error message displays in the Notification area (defined
        as part of the page template).
      * On Error Page - Error
        displays on a separate error page.
6. Click Save.

See Also:

Page Templates

---

<!-- fonte: htmdb/understanding-validations.html -->
## Understanding Validations

Use validations to create edit checks on specific items, pages, or columns.

* About Validations
  Learn about validations.
* What Happens When a Validation Fails?
  Learn what happens when a validation fails.
* Creating a Validation
  Create validations in Page Designer.
* Editing a Validation
  Edit validations in Page Designer.
* About Determining When Validations Execute
  Determine when a validation executes by editing the Always Execute attribute.
* About Defining How Validation Error Messages Display
  Control how validation messages display by editing the Error Message and Error Message attributes.
* Processing Validations Conditionally
  Control when and if a validation executes by configuring the Server-side Condition attributes.
* About Altering the Go to Error Link
  Alter the Go to Error text to change the default text or to translate it into a language that is not translated by default.

### About Validations

Learn about validations.

A validation is an edit check. Validations specific to a single item are page item validations. Validations that apply to an entire page are page validations. Validations for tabular forms specific to a single column are column level validations. Validations for tabular forms that do not apply to a single column are tabular form row validations.

You can define a validation declaratively by selecting a validation method. You enter the actual validation edit check in the Validation Messages field. Be aware that if a validation fails, subsequent page processes or computations do not occur. Also remember that the validation you enter must be consistent with the validation type you selected.

### What Happens When a Validation Fails?

Learn what happens when a validation fails.

If a page is submitted and some of the validations fail, Oracle APEX redisplays the existing page with all inline validation errors. While displaying inline errors, APEX does not execute computations, application processes, or page processes (for example, Automated Row Fetch) which are defined to execute during Page Rendering (in other words, all "On Load %" display points). The one exception is if the computations and processes use the condition type Inline Validation Errors Displayed.

The reason for skipping these computations and processes is that any of they could potentially alter the data entered by the user. For example, an Automated Row Fetch process would fetch and overwrite the modified data with the values from the database when the user actually wants to get the entered data in order to fix the validation error.

If a computation is skipped, the following displays in the debug output:

```sql
Do not perform computation because inline validation errors found.
```

If an application or page process is skipped, the following displays in the debug output:

```sql
Skip because inline validation errors found.
```

### Creating a Validation

Create validations in Page Designer.

Note:

Text entered for validations may not exceed 3,950 characters.

To create a validation in Page Designer:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. Click the Processing tab in the left pane.
3. Right-click Validations and select Create Validation.

   Validation attributes display in the Property Editor. Attributes are organized in groups.

   Note:

   To find a group or attribute, enter keywords in the Filter Properties
   field. The Property Editor displays the group or attributes. Or, you can
   click Go to Group and select the group.
4. Identification, Name - Enter the
   name of the validation. Make this name should be descriptive so that developers
   can easily identify conditions being checked.
5. Execution Options, Sequence -
   Enter the sequence for this validation. The sequence determines the order of
   execution.
6. Edit the following Validation attributes:
   1. Validation, Editable
      Region - Select the associated region.
   2. Validation, Type - Select
      the type of equality to be tested for this validation. Depending on your
      selection, one or more additional attributes are required to fully
      define this validation.

      If the validation passes the equality test, or evaluates to
      TRUE, then the validation error message does not display. Validation
      error messages display when the validation fails the equality test, or
      evaluates to FALSE, or a non-empty text string is returned.
   3. Validation, Always
      Execute - Specify whether this validation always
      executes.

      If set to On, this validation is always
      evaluated, irrespective of the Execute Validations setting defined
      against the button that submitted the page. If set
      to Off, this validation is only evaluated if
      the triggering button has an Execute Validations setting
      of On.
7. Edit the following Error attributes:
   1. Error, Error Message -
      Enter text for the error message.
   2. Error, Display Location -
      Select where the error message displays for this validation.

      Validation error messages display on a separate error page, or
      inline with the existing page. Inline error messages display underneath
      the Associated Item label and/or in a Notification area, defined as part
      of the page template.
   3. Error, Associated Item -
      Select the item where this validation error message displays.

      If you select an item and the Error message display
      location includes Inline with Field, the error
      message displays underneath the label of the specified item. If
      the Error message display location does not include Inline
      with Field, this attribute has no impact on the display
      of the error message.
8. Click Save.

See Also:

* Creating Pre-Rendering Branches, Computations, and Processes
* Creating Page Submission Branches, Validations, Computations, and Processes

### Editing a Validation

Edit validations in Page Designer.

To edit a validation in Page Designer:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. Click the Processing tab in the left pane.
3. Expand Validating and then Validations and select the validation.

   Validation attributes display in the Property Editor. Attributes are
   organized in groups.

   Note:

   To find a group or attribute, enter keywords in the Filter
   Properties field. The Property Editor displays the group or attributes.
   Or, you can click Go to Group and select the
   group.
4. In the Property Editor, edit the appropriate attributes.

   Tip:

   To learn more about an attribute, select the attribute in the Property Editor and click the Help tab in the center pane.
5. Click Save.

### About Determining When Validations Execute

Determine when a validation executes by editing the Always Execute attribute.

The Always Execute attribute determines if validations execute
when a page is submitted. Use this attribute for buttons or certain page items that
submit a page. The Always Execute attribute has two options:

* On - The validation always executes independent of validation
  settings for buttons or items on a page.

  For example, select On if your validation is a security check
  which determines if the current user is allowed to modify or delete the current
  record. This ensures the validation executes for any operation and prevents
  unprivileged users from modifying data.
* Off - The validation only executes if the button or item used
  to submit the page has the Execute Validations attributes
  set to On.

  For example, it is not useful to verify that an item be numeric and display an error
  message if the user is simply deleting a record. In that scenario, the
  validations should only execute when the user clicks the Create or Apply Changes
  buttons.

  To accomplish this behavior:

  + For the validation, set Always Execute to On
  + For the Create and Apply Changes buttons, set Execute Validations to On.
  + For the Delete button, set Execute Validations to Off to avoid unnecessary validations.

See Also:

Editing a Validation

### About Defining How Validation Error Messages Display

Control how validation messages display by editing the Error Message and
Error Message attributes.

You can choose to have validation error messages display inline (that is, on the page where the validation is performed) or on a separate error page.

You define how a validation error message displays by configuring the following validation attributes:

1. Error, Error Message - Enter the error message text in this field. You can use `#LABEL#` as placeholder for the label of the associated page item or `#COLUMN_HEADER#` for the heading of the associated editable region column. The placeholders are not supported if error display location is set to On Error Page.
2. Error, c - Select where the error
   message displays for this validation. Validation error messages display on a
   separate error page, or inline with the existing page. Inline error messages
   display underneath the Associated Item label and/or in a Notification area,
   defined as part of the page template.

   Options include:

   * Inline with Field and in Notification - Error displays inline within the field label and within a notification area (defined as part of the page template).
   * Inline with Field - Error displays inline within the field label.
   * Inline in Notification - Error displays inline within a notification area (defined as part of the page template).
   * On Error Page - Displays the error on a separate error page. To create a hard error that stops all processing (including validations), you must display the error on an error page.
3. Error,
   Associated Item (or Column)
   - Select the item (or column) where this
   validation error message displays.

   If you select an item and the Error message display location includes Inline with Field, the error message displays underneath the label of the specified item. If the Error message display location does not include Inline with Field, this attribute has no impact on the display of the error message.

See Also:

Editing a Validation

### Processing Validations Conditionally

Control when and if a validation executes by configuring the Server-side Condition
attributes.

You can control when and if a validation executes by configuring the following
Server-side Condition attributes:

1. Server-side Condition, When Button
   Pressed - If you want this page processing component to execute
   only when the specified button is clicked, select a button from the list. You
   can incorporate this button condition with other conditions to further refine
   when this page processing component executes.

   If no button is pressed, other conditions are evaluated before
   performing the validation.
2. Server-side Condition, Type -
   Select a condition type from the list that must be met in order for this
   component to be rendered or processed.

   To view a list of options, select the Type
   attribute in the Property Editor and click the Help tab
   in the central pane.

See Also:

* Editing a Validation
* Understanding Conditional Rendering and Processing

### About Altering the Go to Error Link

Alter the Go to Error text to change the default text or to translate it into a
language that is not translated by default.

If you define an associated item, Oracle APEX renders a Go to Error link in the Notification display location next to the corresponding error message. When clicked, the user's focus is set to the associated item.

You can alter the Go to Error text to change the default text or to translate it into a language that is not translated by default with APEX. In either case, define a text message called `APEX.GO_TO_ERROR` with the text and language of your choice. Additionally, you can disable this functionality and remove the Go to Error link by setting the text of the `APEX.GO_TO_ERROR` text message to just a single space.

See Also:

Translating Messages Used Internally by APEX

---

<!-- fonte: htmdb/validation-errors-display-as-apex-errors-automatically.html -->
## Validation Errors Display as APEX Errors Automatically

Learn about the display of validation errors.

When an end user saves changes to a page, any region based on a BOSS REST Data Source
will automatically report any validation errors as an APEX error. The user therefore sees validation failures raised by server-side business
object validation rules or triggers in the same, familar way they are used to seeing
error messages defined inside the APEX application itself. Multiple error messages will each appear on a new line in the
APEX error message.

---

<!-- fonte: htmdb/understanding-page-computations.html -->
## Understanding Page Computations

Use computations to assign a value to an identified item when a page is submitted or displayed.

* About Page Computations
  A page computation assigns a value to an identified item when a page is displayed or submitted (rendered and processed).
* Creating a Page Computation
  Create a Page Computation in Page Designer.
* Editing Page Computation Attributes
  Edit a page computation in Page Designer.
* Editing the Computation Point and Source
  Control when a computation executes by editing the Sequence and Point attributes.
* Example: Computation Points and Computation Syntax
  View computation points and computation syntax example.

See Also:

Understanding Application Computations

### About Page Computations

A page computation assigns a value to an identified item when a page is displayed or
submitted (rendered and processed).

You create a page computation by running the Create Page Computation Wizard. For
each computation, specify the item for which you are creating the computation and a
computation type.

You can also use application-level computations to assign values to items. Most page-level computations populate page items. In contrast, most application-level computations populate application items.

### Creating a Page Computation

Create a Page Computation in Page Designer.

To create a page computation:

1. Navigate to the appropriate page in Page Designer.
2. In the Rendering tab, expand the Pre-Rendering or Post-Rendering node and locate where the computation should be.
3. Right-click the location and select Create Computation.

   Page Designer appears.

   In the Property Editor, attributes are organized into groups. To find a group or attribute, enter keywords in the Filter Properties field. The Property Editor displays the group or attributes. Or, you can click Go to Group and select the group.

   Tip:

   To learn more about an attribute, select the attribute in the Property Editor and click the Help tab in the central pane.
4. Edit the following attributes:
   1. Identification, Item Name - Enter the page or application item populated by this computation.
   2. Execution Options, Sequence - Specify the sequence for this computation. The sequence determines the order of execution.
   3. Execution Options, Point - Select at what point in page rendering or processing this computation is executed. The most typical computation point is After Submit.
   4. Computation, Type - Select a computation type. To view a list of options, see Help.
5. Click Save.

See Also:

* Viewing a Page in Page Designer
* Creating Pre-Rendering Branches, Computations, and Processes
* Creating Page Submission Branches, Validations, Computations, and Processes

### Editing Page Computation Attributes

Edit a page computation in Page Designer.

To edit a page computation:

1. View the page in Page Designer.
2. In the Rendering tab, expand the Pre-Rendering or Post-Rendering node and select the computation.

   Page Designer appears.

   In the Property Editor, attributes are organized into groups. To find a group or attribute, enter keywords in the Filter Properties field. The Property Editor displays the group or attributes. Or, you can click Go to Group and select the group.
3. In the Property Editor, edit the appropriate attributes.

   Tip:

   To learn more about an attribute, select the attribute in the Property Editor and click the Help tab in the center pane.
4. Click Save.

See Also:

Viewing a Page in Page Designer.

### Editing the Computation Point and Source

Control when a computation executes by editing the Sequence and Point
attributes.

You control when a computation executes by editing the Sequence and Point attributes. The Sequence attribute determines the order of evaluation. The Point attribute determines the point in page rendering or processing at which the computation executes. The most typical computation point is After Submit.

To edit a computation point and source:

1. View the page in Page Designer.
2. In the Rendering tab, expand the Pre-Rendering or Post-Rendering node and select the computation.

   Page Designer appears.

   In the Property Editor, attributes are organized into groups. To find a group or attribute, enter keywords in the Filter Properties field. The Property Editor displays the group or attributes. Or, you can click Go to Group and select the group.
3. In the Property Editor, edit the following attributes.
   1. Execution Options, Sequence - Specify the sequence for this component. The sequence determines the order of execution. If two components have the same sequence value, then they may be executed in a different order when the application is exported and imported into another environment.
   2. Execution Options, Point - Select at what point in page rendering or processing this computation is executed.

      For example, selecting On New Instance executes the computation when a new session (or instance) is generated. The most typical computation point is After Submit.
   3. Computation - Define expression or query to compute an item's value.
   4. Error, Error Message - Enter an error message that displays if this computation fails.

   Tip:

   To learn more about an attribute, select the attribute in the Property Editor and click the Help tab in the center pane.
4. Click Save.

See Also:

Viewing a Page in Page Designer

### Example: Computation Points and Computation Syntax

View computation points and computation syntax example.

A good example of using computations can be illustrated by a page containing form fields for entering phone numbers. In this example, the phone number is stored in one database column; however, the data entry form breaks the phone number into three components: area code, prefix, and line number. In this example, the page items are called `P10_AREA_CODE`, `P10_PREFIX`, and `P10_LINE_NUMBER`.

Next, suppose you need to combine the values stored in these items into a single string. You could accomplish this by using an After Submit computation and store the combined values in an item called `P10_PHONE_NUMBER`.

To create a computation to store the combined values of `P10_AREA_CODE`, `P10_PREFIX`, and `P10_LINE_NUMBER` in new items:

1. Navigate to the appropriate page.
2. Create an item named `P10_PHONE_NUMBER` to store the combined values of `P10_AREA_CODE`, `P10_PREFIX`, and `P10_LINE_NUMBER`.
3. Create the computation:
   1. In the Rendering tab, expand the Pre-Rendering.
   2. Select a location, and then right-click and select Create Computation.

      Page Designer appears.

      In the Property Editor, attributes are organized into groups. To find a group or attribute, enter keywords in the Filter Properties field. The Property Editor displays the group or attributes. Or, you can click Go to Group and select the group.

      Tip:

      To learn more about an attribute, select the attribute in the Property Editor and click the Help tab in the central pane.
4. In the Property Editor, edit the following attributes:
   1. Identification, Item Name - Select `P10_PHONE_NUMBER`.
   2. Execution Options, Sequence - Specify the sequence for this computation. The sequence determines the order of execution.
   3. Execution Options, Point - Select at what point in page rendering or processing this computation is executed. The most typical computation point is After Submit.
5. For Computation Type, you can create the following computation types:
   1. Static Value:

      * Computation, Type - Select Static Value .
      * Computation, Static Value - Enter the following computation:

        ```sql
        (&P10_AREA_CODE.) &P10_PREFIX.-&P10_LINE_NUMBER.
        ```
   2. PL/SQL Function Body:

      * Computation, Type - Select PL/SQL Function Body .
      * Computation, PL/SQL Function Body - Enter the computation:

        ```sql
        DECLARE
        l_return_value  VARCHAR2(300) DEFAULT NULL;
        BEGIN
            l_return_value :=
        '('||:P10_AREA_CODE||')'||:P10_PREFIX||'-'||:P10_LINE_NUMBER;
        RETURN l_return_value;
        END;
        ```
   3. SQL Query (return colon separated value):

      * Computation, Type - Select SQL Query (return colon separated value) .
      * Computation Type, SQL Query - Enter the computation:

        ```sql
        SELECT '('||:P10_AREA_CODE||')'||:P10_PREFIX||'-'||:P10_LINE_NUMBER FROM DUAL
        ```
   4. PLSQL Expression:

      * Computation, Type - Select PLSQL Expression .
      * Computation Type, PLSQL Expression - Enter the computation:

        ```sql
        '('||:P10_AREA_CODE||')'||:P10_PREFIX||'-'||:P10_LINE_NUMBER
        ```
6. Click Save.

See Also:

About the Differences Between Page Items and Application Items

---

<!-- fonte: htmdb/understanding-application-computations.html -->
## Understanding Application Computations

Create an application computation to set the value of a single page or application-level item. Application computations run at the same point across multiple pages in an application.

Tip:

To learn more about execution behavior in the case of a validation error, see What Happens When a Validation Fails?

* About Application Computations
  Application Computations are units of logic that set the value of a single page or application-level item and are run at the same point across multiple pages in an application.
* About Application Computations that Execute On New Instance
  Use the On New Instance Computation Point to retrieve information once within a user's session.
* Creating an Application Computation
  Create an application computation from Shared Compoents.
* Copying or Subscribing to Application Computations
  Copy application computations from the current application or from another application. When copying an application computation from another app, you can also subscribe to it.
* Subscribing to an Application Computation
  Subscribe to an application computation on the Application Computations, Create / Edit page.
* Accessing the Application Computation History Report

### About Application Computations

Application Computations are units of logic that set the value of a single page or
application-level item and are run at the same point across multiple pages in an application.

Similar to page-level computations, application computations can be based on static
values, item values, PL/SQL, or SQL. A common use of an application item is to store the
value of the last page viewed in the application. By storing the value in an item, you can
add a back button and then redirect the user to the page number captured by the
computation. This type of computation works well, for example, when you need to enable
users to back out of an error page.

Example: Storing the Last Visited Page

The following is
an example of a computation that stores the last page visited. In this example, the
computation:

* Stores the last application page visited to an item named
  `LAST_PAGE`
* Checks that the value of a `CURRENT_PAGE_ITEM` is of
  type PL/SQL Function Body with a Computation body of:

  ```sql
  BEGIN
     :LAST_PAGE := nvl(:CURRENT_PAGE,:APP_PAGE_ID);
     :CURRENT_PAGE := :APP_PAGE_ID;
     RETURN :LAST_PAGE;
  END;
  ```

v

### About Application Computations that Execute On New Instance

Use the On New Instance Computation Point to retrieve information once within a user's session.

Typically an application computation runs at the same point across multiple pages in
an application. The exception is computations having a Computation
Point of On New Instance. These types of
computations are useful when you only need to retrieve information once within a user's
session. For example, if the application items do not depend on the logged in user, you
can initialize them using the Computation Point On New Instance.
To look up information that depends on the user, you can also use After
Authentication.

If you configure applications to share the same session by setting the same cookie name in the authentication scheme, On New Instance and After Login, the application processes fire whenever Oracle APEX first processes a request for the application (that is, On New Instance), or processes a request of an authenticated user for the application (that is, After Authentication).

### Creating an Application Computation

Create an application computation from Shared Compoents.

To create an application computation:

1. Navigate to the Shared Components page:
   1. On the Workspace home page, click App
      Builder.
   2. Select an application.
   3. On the Application home page, click Shared Components.

      The Shared Components page appears.
2. Under Application Logic, select Application Computations.
3. Click Create.
4. Edit the following attributes:
   1. Item, Sequence - Specify
      the sequence for this component. The sequence determines the order of
      evaluation.
   2. Item, Computation Item -
      Select the item this computation affects.
   3. Frequency, Computation
      Point - Select a process point at which this computation
      should be performed. Selecting After Submit
      causes the computation to be performed only after the page is displayed
      and then submitted.
   4. Computation, Computation
      Type - Select the manner in which this computation is
      performed.
   5. Computation, Computation
      - Enter the computation logic that corresponds to the computation type.
      See field-level Help for examples.
   6. Computation, Computation Error
      Message - Enter the error message that displays if the
      computation fails.
   7. Authorization, Authorization
      Scheme (optional) - Select an authorization scheme which
      must evaluate to True in order for this computation to execute.
   8. Conditions, Condition Type (optional) - Select a condition type that must be met in order for this computation to execute.
   9. Configuration, Build Option (optional) - Select a build option for this component.
   10. Comments, Comments (optional) - Enter any comments.
5. Click Create Computation.

See Also:

Using Build Options to Control Configuration

### Copying or Subscribing to Application Computations

Copy application computations from the current application or from
another application. When copying an application computation from another app, you can also
subscribe to it.

Tip:

Subscriptions enable developers to reuse shared components across
several applications in a workspace. To learn more about subscriptions, see Using Shared Component Subscriptions.

Note:

When copying an application computation from another app, shared component
dependencies are automatically resolved. To learn more, see About Automatic Dependency Resolution.

To copy or subscribe to an application
computation:

1. Navigate to the application computations page.
   1. Navigate to the Workspace home page.
   2. Click the App
      Builder icon.
   3. Select an application.
   4. On the Application home page, click Shared
      Components.
   5. Under Application Logic, click Application
      Computations.

      The Application Computations page appears. Note that the
      report includes the following columns: Subscribed From, Subscription
      Status, and Subscribers.
2. To copy an application computation within the current application:
   1. Search for the application computation and click
      Copy in the Copy column.

      The Copy Application Computation Wizard appears.
   2. New Computation Item - Select an application-level or a page-level
      item.
   3. Click Copy Application Computation.
3. To copy an application computation from another application:
   1. From the Tasks region, click Copy from another
      app.

      The Copy Application Computation Wizard appears.
   2. Application - Select the application from which you want to copy.
   3. Copy Application Computation - Select the application computation to
      copy.
   4. Subscribe - Set this flag to On to subscribe to
      the application computation.
   5. Click Copy Application Computation.

### Subscribing to an Application Computation

Subscribe to an application computation on the Application Computations,
Create / Edit page.

Subscriptions enable developers to reuse shared components across several
applications in a workspace. To learn more about shared component subscriptions, see
Using Shared Component Subscriptions.

Tip:

You can also subscribe
to a search configuration by copying it and then subscribing. See Copying or Subscribing to Application Computations.

To subscribe to an application computation:

1. Navigate to the Application Computations page:
   1. On the Workspace home page, click App
      Builder.
   2. Select an application.
   3. On the Application home page, click Shared
      Components.

      The Shared Components page appears.
   4. Under Application Logic, click Application
      Computations.

      The Application Computations page appears. Note that the
      report includes the following columns: Subscribed From, Subscription
      Status, and Subscribers.
2. Select an application computation.

   The Application Items, Create / Edit page
   appears.
3. To subscribe to an application computation:
   1. Find the Subscription region.
   2. Subscription, Subscribe From - Select a master application computation
      to subscribe to and click Apply
      Changes.

      The subscribed component is automatically refreshed from
      the selected master.
4. To refresh a subscribed application computation:
   1. Find the Subscription region.
   2. Subscription, Refresh Application Computation - If the application
      computation is already subscribed, click Refresh Application
      Computation.
5. To unsubscribe from a subscribed application computation:
   1. Find the Subscription region.
   2. Subscription, Unsubscribe - Click
      Unsubscribe.

### Accessing the Application Computation History Report

Once you create an application computation, you can view the Application
Computation History report. The Application Computation History report displays a
history of recently changed application computations by date.

To access the Application Computation History report:

1. Navigate to the Shared Components page:
   1. On the Workspace home page, click App
      Builder.
   2. Select an application.
   3. On the Application home page, click Shared Components.

      The Shared Components page appears.
2. Under Application Logic, select Application Computations.
3. Select the History at the top of the page.
4. You can customize the appearance the page using the Search bar at the top of the page. Available controls include:

   * Select columns to search - Resembles a magnifying glass. Click this icon to narrow your search. To search all columns, select All Columns.
   * Text area - Enter case insensitive search criteria (wildcard characters are implied) and click Go.
   * Go button - Executes a search or applies a filter.
   * Actions menu - Use the Actions menu to customize the report view.

See Also:

About the Actions Menu

---

<!-- fonte: htmdb/about-branches.html -->
## About Branches

A branch is an instruction to go to a specific page, procedure, or URL. For example, you can branch from page 1 to page 2 after page 1 is submitted. When you create a branch, you specify a Branch Point and Branch Type.

See Also:

Controlling Navigation Using Branches

---

<!-- fonte: htmdb/controlling-navigation-using-branches.html -->
## Controlling Navigation Using Branches

Add navigation to application pages by creating branches. A branch is an instruction to link to a specific page, procedure, or URL after a given page is submitted.

* Creating a Branch
  Create a branch in Page Designer.
* About Branching Conditionally
  Make a branch conditional by editing Server-side Condition attributes in Page Designer.

See Also:

Accessing Page Specific Utilities

### Creating a Branch

Create a branch in Page Designer.

To create a branch:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. Create a branch in the left pane:
   * Rendering tab - Right-click and
     select Create Branch
   * Processing tab - Right-click and
     select Create Branch.

   The Property Editor displays the Branch attributes.
3. Page Designer indicates what to do next. If there is an error, the Show
   Messages icon displays in the Page Developer toolbar.
   1. Click the Show Messages icon on the Page
      Designer toolbar.

      The Messages dialog displays errors that must be
      addressed.
   2. Select an error to highlight the associated attribute in the Property
      Editor.
4. In the Property Editor, edit the attributes:

   Tip:

   To learn more about an attribute, select the attribute in
   the Property Editor and click the Help tab in the central
   pane.

   1. Identification, Name -
      Specify the name of the branch for easy identification by
      developers.
   2. Execution Options:

      1. Sequence - Specify the
         sequence for this component. The sequence determines the
         order of execution.
      2. Point - Select the point
         in the processing at which this branch action is considered.
         Options include:

         * After Submit
           (previously named Before
           Computation)
         * Validating
           (previously named Before
           Validation)
         * Processing
           (previously named Before
           Processing)
         * After Processing
           (previously named After
           Processing)
         * Before Header
           (previously named Before
           Header)
   3. Behavior, Type - Select a
      page branch type. To learn more, click the Help
      tab in the central pane.

      The attributes that display in the Property Editor depend
      on the branch type you select.

      If Type is Page or URL
      (Redirect), click Target and edit
      the attributes in the Link Builder Target dialog.
   4. Server-Side Condition:

      1. When Button Pressed - If
         you want this page processing component to execute only when
         the specified button is clicked, select a button from the
         list. You can incorporate this button condition with other
         conditions to further refine when this page processing
         component executes.
      2. Condition Type - Select a
         condition type from the list that must be met in order for
         this component to be rendered or processed. To learn more,
         click the Help tab in the central
         pane.
5. Click Save.

See Also:

* About the When Button Pressed Attribute
* Creating Pre-Rendering Branches, Computations, and Processes
* Creating Page Submission Branches, Validations, Computations, and Processes

### About Branching Conditionally

Make a branch conditional by editing Server-side Condition attributes in
Page Designer.

To make a branch conditional, view the branch attributes in the Property Editor.
Under Server-side Condition, edit the appropriate attributes.

---

<!-- fonte: htmdb/available-conditions.html -->
## E Available Conditions

Learn about conditions available in App Builder.

* What Are Conditions?
  Learn about conditions.
* Conditions Available in App Builder
  Review descriptions of conditions available in Oracle APEX.

**Related Topics**

* Understanding Conditional Rendering and Processing

### E.1 What Are Conditions?

Learn about conditions.

A condition is a small unit of logic that
helps developers control the display of regions, items, buttons, and tabs as well
execute processes, computations and validations. When you apply a condition to a
control or component, the condition is evaluated. Whether a condition passes or
fails determines whether a control or component displays, or page processing
executes.

You can specify conditions by selecting a condition
type when you create the control (region, button, or item) or component (tab, list,
or navigation bar), or by making a selection under the condition attribute.

### E.2 Conditions Available in App Builder

Review descriptions of conditions available in Oracle APEX.

Tip:

To view a complete listing of all available conditions for a given
control or component, expand the condition type list.

| Condition | Description |
| --- | --- |
| Rows returned | The SQL query returns one or more rows. |
| No Rows returned | The SQL Query returns no rows |
| SQL Expression | The SQL expression evaluates to TRUE. |
| PLSQL Expression | The SQL expression evaluates to TRUE. |
| PL/SQL Function Body | The PL/SQL function body returns TRUE. |
| Request = Value | The page request is equal to the text you enter into the Value attribute. |
| Request != Value | The page request is not equal to the text you enter into the Value attribute. |
| Request is contained in Value | The page request is contained in the text you enter into the Value attribute. |
| Request is NOT contained in Value | The page request is not contained in the text you enter into the Value attribute. |
| Item = Value | The value of the selected item is equal to the text you enter into the Value attribute. |
| Item != Value | The value of the selected item is not equal to the text you enter into the Value attribute. |
| Item is NULL | The value of the selected item is empty. |
| Item is NOT NULL | The value of the selected item is not empty. |
| Item is zero | The value of the selected item is the number zero. |
| Item is NOT zero | The value of the selected item is not the number zero. |
| Item is NULL or zero | The value of the selected item is empty or the number zero. |
| Item is NOT NULL and NOT zero | The value of the selected item is not empty and not the number zero. |
| Item contains no spaces | The value of the selected item has no spaces. |
| Item is numeric | The value of the selected Item is numeric. |
| Item is NOT numeric | The value of the selected item is not numeric. |
| Item is alphanumeric | The value of the selected item is alphanumeric, containing only letters or numbers and no special characters. |
| Item is in colon delimited list | The value of the selected item is completely contained in the text you enter into the Value attribute. |
| Item is NOT in colon delimited list | The value of the selected Item is not completely contained in the text you entered into the Value attribute. |
| User Preference = Value | The value of the Preference entered is equal to the text you enter into the Value attribute. |
| User Preference != Value | The value of the Preference entered is not equal to the text you enter into the Value attribute. |
| Current Page = Page | The current page is equal to the value you enter into Page. |
| Current Page != Page | The current page is not equal to the value you enter into Page. |
| Current Page is in comma delimited list | The current page is in the comma separated list you enter into Pages. |
| Current Page is NOT in comma delimited list | The current page is not in the comma separated list you enter into Pages. |
| Current page is in Printer Friendly mode | The current page has been toggled to 'Printer Friendly Mode' by the end user. |
| Current page is NOT in Printer Friendly mode | The current page has not been toggled to 'Printer Friendly Mode' by the end user. |
| Page/Region is Read Only | Either the page or parent region, if appropriate, 'Read Only' condition evaluates to TRUE. |
| Page/Region is NOT Read Only | The page and parent region, if appropriate, are displayed normally. |
| User is authenticated (not public) | The end user is logged into the application.  See Also: Establishing User Identity Through Authentication for information about authentication |
| User is the public user (user has not authenticated) | The end user is not logged into the application. |
| Inline Validation Errors Displayed | An inline validation error is displayed on the page, following a page submission. |
| Inline Validation Errors NOT displayed | An inline validation error is not displayed on the page. |
| Current Language = Value | The end user is currently running the application in the language you enter into the Value attribute. |
| Current Language != Value | The end user is not currently running the application in the language you enter into the Value attribute. |
| Current Language is contained in Value | The end user is currently running the application in one of the languages you enter into the Value attribute. |
| Current Language is NOT contained in Value | The end user is not currently running the application in one of the languages you enter into the Value attribute. |
| Never | The component is never rendered.  Note: Changing a condition to Never will remove any existing condition. For temporarily disabling a component, Oracle recommends using the Build Option attribute. |
