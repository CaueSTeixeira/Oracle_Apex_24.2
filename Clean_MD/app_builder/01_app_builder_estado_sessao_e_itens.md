# 01_app_builder_estado_sessao_e_itens
Fonte: Oracle APEX 24.2 App Builder User's Guide — https://docs.oracle.com/en/database/oracle/apex/24.2/htmdb/

<!-- fonte: htmdb/understanding-session-state-management.html -->
## Understanding Session State Management

Oracle APEX transparently maintains session state and provides developers with the ability to get and set session state values from any page in the application.

* What is Session State?
  Session state enables developers to store and retrieve values for a user as the user navigates between different application pages.
* About Session IDs
  A session ID is a unique number assigned a specific user for the duration of that user's visit (or session).
* What Is a Session?
  A session is a logical construct that establishes persistence (or stateful behavior) across page views.

### What is Session State?

Session state enables developers to store and retrieve values for a user as
the user navigates between different application pages.

Hypertext Transfer Protocol (HTTP), the protocol over which HTML pages are most often delivered, is a stateless protocol. A web browser is only connected to the server for as long as it takes to download a complete page. Each page request is treated by the server as an independent event, unrelated to any page requests that happened previously or that may occur in the future. To access form values entered on one page on a subsequent page, the values must be stored as session state. Oracle APEX transparently maintains session state and provides developers with the ability to get and set session state values from any page in the application.

### About Session IDs

A session ID is a unique number assigned a specific user for the duration of
that user's visit (or session).

The Oracle APEX engine establishes the identity of the user for each page request and the session ID
to fetch session state from the database. The most visible location of the session ID is
in the URL for a page request:

* The third parameter in the f?p URL Syntax:

  ```sql
  https://apex.example.com/ords/f?p=392:3:13766599855150
  ```
* The `session` parameter in the Friendly URL
  Syntax::

  ```sql
  https://apex.example.com/ords/mycompany/r/hr-app/update-employees?session=13766599855150
  ```

In both examples, the session ID is `13766599855150`.

Another visible location is in the page's HTML POST data and indirectly in the contents of a session cookie. This cookie is sent by the APEX engine during authentication and is maintained for the life of the application (or browser) session.

APEX assigns new session IDs during authentication processing, records the authenticated user's identity with the session ID, and continually checks the session ID in each page request's URL or POST data with the session cookie and the session record in the database. These checks provide users with flexibility and security.

While the session ID is the key to session state, the session cookie and the session record safeguard the integrity of the session ID and the authentication status of the user.

See Also:

Understanding URL Syntax

### What Is a Session?

A session is a logical construct that establishes persistence (or stateful
behavior) across page views.

Each session is assigned a unique identifier. The Oracle APEX engine uses this identifier (or session ID) to store and retrieve an application's
working set of data (or session state) before and after each page view. Because sessions
are entirely independent of one another, any number of sessions can exist in the
database at the same time. A user can also run multiple instances of an application
simultaneously in different browser programs.

Sessions are logically and physically distinct from Oracle database sessions used to service page requests. A user runs an application in a single APEX session from sign in to sign out with a typical duration measured in minutes or hours. Each page requested during that session results in the APEX engine creating or reusing an Oracle database session to access database resources. Often these database sessions last just a fraction of a second.

See Also:

Viewing Active Sessions in Oracle APEX
Administration Guide

---

<!-- fonte: htmdb/managing-session-state.html -->
## Managing Session State

View session state and manage session state overrides from the Runtime Developer toolbar which displays at the bottom of any editable page at runtime.

* Viewing Session State
  View the Session page at runtime by clicking Session and then View Session State on the Runtime Developer toolbar.
* Managing Session State Overrides
  Access the Session Overrides dialog from the Runtime Developer tool bar to manage session state values at runtime.

See Also:

* Runtime Developer Toolbar
* Understanding Page Items
* Managing Application Items
* About Using Collections
* Using Substitution Strings for information about referencing item values

### Viewing Session State

View the Session page at runtime by clicking Session and then View Session
State on the Runtime Developer toolbar.

The Session page provides valuable information about the session in which the application is currently running. Must of the behavior of an Oracle APEX application is driven by values in session state. For example, a button may display conditionally based on the value of an item session state. This section describes how to view session state for a page.

To view the Session page:

1. Run the application as a developer.
2. Locate the Runtime Developer toolbar. By default, the Runtime Developer toolbar
   displays at the bottom of the page.

   Description of the illustration toolbar.png
3. On the Runtime Developer toolbar, click Session and then
   View Session State.

   The Session page appears and displays the following information
   displays at the center of the page.

   * Application - Identifies the
     application name.
   * Session - Displays the session ID
     for the current session.
   * User - Identifies the current
     user.
   * Workspace - Displays the current
     workspace ID.
   * Browser Language - Identifies the
     current browser language.
4. Configure the fields at the top of the page and click
   Set to alter the display:
   * Page - Locate a page. Enter a page
     number.
   * Find - Enter a case insensitive
     query. Use Find to search item name and item value, or collection name
     (depending upon your view).
   * Rows - Select the number of items to
     display.
   * View - Select a session state report
     to view.

### Managing Session State Overrides

Access the Session Overrides dialog from the Runtime Developer tool bar
to manage session state values at runtime.

The Session Overrides switch eanbles you to enable
or disable all session values. Likewise, every session value has a switch that
enables you control session state value overrides.

For example, if you need to translate an application you can change the Application
Language attribute. Another common use case for session overrides is to change the
file path values such as `#APP_FILES#`. This type of change would
redirect the URL to somewhere else, like `localhost:PORT` for local
development.

To access the Session Overrides dialog:

1. Run the application as a developer.
2. Locate the Runtime Developer toolbar. By default, the Runtime Developer toolbar
   displays at the bottom of the page.
3. On the Runtime Developer toolbar, click Session and then
   Session Overrides.
4. In the Session Overrides dialog:
   1. Enable Sessions Overrides - Use this switch to enable or disable all
      session values.
   2. Globalization:

      * Application Language - Change the language of the
        current application for the current user.
      * Document Direction- Change the document direction
        (Left to Right, Right to Left) of the current application
        for the current user
      * Timezone - Change the timezone of the current
        application for the current user.

      You can also edit these attributes in Globalization
      attributes. See Configuring Globalization Attributes.
   3. File Paths:

      * Application Files
        `#APP_FILES#` - Enable this option
        to change the value of `#APP_FILES#` to point
        to another location. `#APP_FILES#` determines
        the virtual path the web server uses to point to the images
        directory distributed with App Builder. During installation, the virtual path is configured as
        `/i/` . If you are unsure, contact your
        administrator.

        You can also edit this attribute in User Interface, Advanced.
        See Editing User Interface Attributes.
      * Workspace Files
        `#WORKSPACE_FILES#` - Enable this
        option to change the value of
        `#WORKSPACE_FILES#` to point to another
        location. `#WORKSPACE_FILES#` references
        uploaded images, JavaScript, and cascading style sheets that
        are shared over many applications within a workspace.
      * Theme Files `#THEME_FILES#`
        - Enable this option to change the value of
        `#THEME_FILES#` to point to another
        location. Use the `#THEME_FILES#` to
        reference files which are stored with your theme
        definition
   4. Additional Files:

      * JavaScript URLs - Load additional JS file URLs
        to this application for the current user.

        You can also edit this attribute in User Interface,
        JavaScript. See Editing User Interface Attributes.
      * CSS URLs - Load additional CSS file URLs to this application
        for the current user.

        You can also edit this attribute in User Interface, CSS. See
        Editing User Interface Attributes.
5. Exit the dialog:
   * Click Save to save your changes.
   * Click Reset to undo any changes.
   * Click Cancel to exist dialog without making any
     changes.

---

<!-- fonte: htmdb/managing-session-state-values.html -->
## Managing Session State Values

Manage session state to store and retrieve values for a user as the user navigates between different application pages.

When building interactive, data-driven web applications, the ability to access and manage session state values is critical. In Oracle APEX, session state is automatically managed for every page and easily referenced in static HTML or logic controls such as processes or validations.

* About Referencing Session State
  Reference item values stored in session state in regions, computations, processes, validations, and branches. An item can be a field, a text area, a password, a select list, or a checkbox.
* About Setting Session State
  Set session state using form submissions, bind variables, computations, or f?p syntax. Session state can also be set using the `APEX_SESSION_STATE.SET` APIs.
* Clearing Session State
  Clearing a cached value resets the value to null. You can clear the cached value for specific items, all items on a page, all pages in an application, or the current user session.
* Referencing Session State Using Bind Variable Syntax
  Use bind variable syntax anywhere where you are using SQL or PL/SQL to reference session state of a specified item.
* About Session Cloning
  Use session cloning to open a new browser window in an Oracle APEX application and have it generate a new distinct session identifier and copy the session values from the original APEX session to the new one.

See Also:

Understanding Session State Management and Referencing Item Values

### About Referencing Session State

Reference item values stored in session state in regions, computations,
processes, validations, and branches. An item can be a field, a text area, a password, a
select list, or a checkbox.

The following table describes the supported syntax for referencing item values.

| Type | Syntax | Description |
| --- | --- | --- |
| SQL | Standard item syntax:  `:MY_ITEM`  Syntax for items containing special characters:  `:"MY_ITEM"` | For items whose names are no longer than 30 characters, precede the item name with a colon (:). Use this syntax for references within a SQL query and within PL/SQL.  To reference page items containing special, multibyte, or unicode characters, wrap the page item name in double quotation marks.  The data type of the bind variable is the Session State Data Type of the item. Most items are `VARCHAR2` by default, but certain item types can be set to `CLOB`. |
| PL/SQL | `V('MY_ITEM')` or `APEX_SESSION_STATE.GET_VARCHAR2('MY_ITEM')` | Use PL/SQL syntax to reference an item value using the `V` function. You can use the shorthand, `V` function, in place of `APEX_SESSION_STATE.GET_VARCHAR2`.  Use this syntax when utilizing Oracle APEX variables directly within an Oracle database object, such as a function, trigger, or Oracle Data Redaction policy.  Tip: When using `V('MY_ITEM')`, `apex_session_state.get_clob('MY_ITEM')` or similar in a SQL query, Oracle recommends using Fast Dual functionality `=> (select v('my_item') from dual)` to improve performance. |
| PL/SQL | `APEX_SESSION_STATE.GET_CLOB('MY_CLOB_ITEM')` | This function returns the value of a `CLOB` page item.  Tip: When using `V('MY_ITEM')`, `apex_session_state.get_clob('MY_ITEM')` or similar in a SQL query, Oracle recommends using Fast Dual functionality `=> (select v('my_item') from dual)` to improve performance. |
| PL/SQL | `APEX_SESSION_STATE.GET_NUMBER('MY_NUMERIC_ITEM')` | This function returns the value of a page item as a `NUMBER`. The item's Format Mask is used to perform the conversion.  Tip: When using `V('MY_ITEM')`, `apex_session_state.get_clob('MY_ITEM')` or similar in a SQL query, Oracle recommends using Fast Dual functionality `=> (select v('my_item') from dual)` to improve performance. |
| PL/SQL | `APEX_SESSION_STATE.GET_TIMESTAMP('MY_NUMERIC_ITEM')` | This function returns the value of a page item as a `TIMESTAMP`. The item's Format Mask is used to perform the conversion.  Tip: When using `V('MY_ITEM')`, `apex_session_state.get_clob('MY_ITEM')` or similar in a SQL query, Oracle recommends using Fast Dual functionality `=> (select v('my_item') from dual)` to improve performance. |
| Static text (exact) | Standard item syntax:  `&MY_ITEM.`  Syntax for items containing special characters:  `&"MY_ITEM".` | For static text or an exact substitution, use the convention `&ITEM_NAME` followed by a period (.).  To reference page items containing special, multibyte, or unicode characters, wrap the page item name in double quotation marks.  Page items of Session State Data Type `CLOB` cannot be references via this syntax. A different output mechanism must be used to fetch their values, such as a page item in Read Only mode, a Display Only page item, or its manual output using a Dynamic Content region. |

See Also:

Changes in Oracle APEX API
Reference in Oracle APEX API
Reference

### About Setting Session State

Set session state using form submissions, bind variables, computations, or
f?p syntax. Session state can also be set using the `APEX_SESSION_STATE.SET`
APIs.

Methods for Setting Session
State

See Also:

Changes in Oracle APEX API Reference in Oracle APEX API
Reference

You can set the value of a page item in your application and therefore
set session state using the following methods:

* Form submission. See the next section.
* Bind variable. See Referencing Session State Using Bind Variable Syntax.
* Computation. See Understanding Application Computations.
* f?p syntax. See About Using f?p Syntax to Link Pages.

About Setting Session State with a Form Submission

When a user submits a page, the Oracle APEX engine automatically stores values typed into fields (items) in session state. For example, suppose you have an application containing two pages. The first page of the application contains a form in which a user can enter a phone number. You defined this form by creating an item named `P1_PHONENO`. On the second page, you want to display the information the user enters in the form.

When the page is submitted, APEX captures the value entered in the phone number field and stores the value for
future use. On the second page, the phone number entered by the user can then be
retrieved from session state using the name `P1_PHONE_NO` with the
appropriate syntax described in About Referencing Session State.

About Controlling How Items Write Session State

You can control whether a page item writes its session state into persistent (disk)
session state or just into memory by configuring the item attribute,
Maintain Session State. Available Maintain Session State
options include:

* Per Request (Memory Only) - Do not save state in the
  database. State is only available when processing the current request. When AJAX
  requests need to use an item, make sure to pass the item name using the Page
  Items To Submit attribute.
* Per Session (Disk) - Maintain for each session by storing
  the value in the database, to access it across requests.
* Per User (Disk) - Value is saved in a user attribute
  repository and it is also available for later APEX sessions.

Note:

When creating database items that work with a Form region (for example as part of
a wizard), Per Request (Memory Only) is the default. Per
User (Disk) is not available for these items.

See Also:

Controlling How Page Items Write Session State

### Clearing Session State

Clearing a cached value resets the value to null. You can clear the cached value for specific items, all items on a page, all pages in an application, or the current user session.

* About Clearing Cache for an Item
  View examples for clearing cache for a single item.
* About Clearing Cache for All Page Items
  View examples for clearing cache for all page items.
* About Clearing Report Regions
  Learn about clearing report cache.
* Clearing Cache for an Entire Application
  View an eample of clearing cache for an application.
* About Resetting an Application Completely
  Learn about resetting an application completely.
* About Clearing Cache for the Current User Session
  View an example of clearing application cache for the current user session.

#### About Clearing Cache for an Item

View examples for clearing cache for a single item.

Clearing cache for a single item resets the value of the item to null. For example,
you might use this approach to make sure a specific item's value is null when a page is
prepared for rendering.

Example 3-4 Example: Clearing Cache for an Item

The following example uses standard `f?p` syntax to clear the cache for an item. This example calls page 5 of application 100. Placing `MY_ITEM` in the `ClearCache` position of the `f?p` syntax resets the value of `MY_ITEM` to `NULL`.

```sql
f?p=100:5:&APP_SESSION.::NO:MY_ITEM
```

The following example resets the value of the items `THE_EMPNO` and `THE_DEPTNO`:

```sql
f?p=100:5:&APP_SESSION.::NO:THE_EMPNO,THE_DEPTNO
```

#### About Clearing Cache for All Page Items

View examples for clearing cache for all page items.

Caching application items is an effective way to maintain session state. However, there are occasions when you may want to clear the cache for all items on a page. For example, suppose you needed to clear all fields on a page when a user clicks a link that creates a new order. By clearing the cache for an entire page, you set the value of all items on the page to null.

Example 3-5 Example: Clearing Cache for Two Pages and Resetting Pagination

This example clears the session cache for two pages and resets pagination.

```sql
f?p=6000:6003:&APP_SESSION.::NO:RP,6004,6014
```

This example:

* Runs page 6003 of application 6000 and uses the current session ID.
* Indicates to not show debug information (`NO`).
* Clears all values maintained by the current session's cache for items of pages 6004 and 6014.
* Resets region pagination (`RP`) on page 6003 (the requested page).

Example 3-6 Example: Clearing Cache on a Page and Passing an Item Value

This example shows how to implement an update form. It clears existing information and sets the item's value (typically a primary key).

```sql
f?p=6000:6003:&APP_SESSION.::NO:6003:MY_ITEM:1234
```

This example:

* Runs page 6003 of application 6000 and uses the current session ID
* Indicates to not show debug information (`NO`)
* Clears all values maintained by the current session's cache for items on page 6003
* Sets the session state of an item called `MY_ITEM` to the value `1234`

Example 3-7 Example: Clearing Session Cache on a Page and Passing Values to Multiple Items

This example demonstrates how to implement an update form. It clears existing information, sets the item's value (typically a primary key), and passes values to multiple items.

```sql
f?p=6000:6004:&APP_SESSION.::NO:6003:MY_ITEM1,MY_ITEM2,MY_ITEM3:1234,,5678
```

This example:

* Runs page 6004 of application 6000 and uses the current session ID
* Clears the current session's cache for items on page 6003
* Indicates to not show debug information (`NO`)
* Sets the value of `MY_ITEM1` to 1234, sets the value of `MY_ITEM2` to null (indicated by the comma used as placeholder), and sets the value of `MY_ITEM3` to 5678

#### About Clearing Report Regions

Learn about clearing report cache.

Report settings can be cached. Depending on the report types, different settings are
cached. Use the following to clear report cache settings:

* `RR` - Resets interactive report, interactive grids, or
  classic report and also resets report pagination. If the target page contains
  interactive report or interactive grids, the report is returned to the default
  report settings specified by the developer or saved by the user. If the target page
  contains classic report, the report sorting resets to developer defined
  sorting.
* `CR` - This applies only to interactive report. `CR` clears interactive report and resets report pagination. This clears all of the session report settings such as control break, aggregate, flashback, chart, number of rows to display, filter, highlight, computation, group by, and pivot.
* `RP` - Resets interactive report or classic report pagination.

Example 3-8 Resetting Report Settings and Pagination

This example resets report settings and pagination of the target page report
regions:

```sql
f?p=6000:6003:&APP_SESSION.::NO:RR
```

Note:

Starting with Oracle APEX release 2.1, you do not need to define separate clear cache syntax to reset report and reset pagination. `RR` will handle both.

#### Clearing Cache for an Entire Application

View an eample of clearing cache for an application.

This example clears the application's cache by using `f?p` syntax and creating a `Clear Cache` argument using the keyword APP.

```sql
f?p=App:Page:Session::NO:APP
```

#### About Resetting an Application Completely

Learn about resetting an application completely.

Resetting the cache for an entire application does not restore the application to a completely reset state. For example, if an application includes on-new instance computations or on-new instance processes, the Oracle APEX engine runs these computations and processes when the application session is created. Then, it processes the clear cache request and displays the requested page.

To reset an application completely without a session ID (if no cookie is used to track the session ID), you must request it using a URL without a session ID, or by calling `APEX_UTIL`.`CLEAR_APP_CACHE` from another application. If the session ID is tracked using a cookie, you must logout to reset the state.

#### About Clearing Cache for the Current User Session

View an example of clearing application cache for the current user
session.

Another approach to clearing an application's cache is to create a `Clear Cache` argument using the keyword `SESSION`. For example:

```sql
f?p=6000:6004:12507785108488427528::NO:SESSION
```

### Referencing Session State Using Bind Variable Syntax

Use bind variable syntax anywhere where you are using SQL or PL/SQL to reference session state of a specified item.

* About Using Bind Variable Syntax
  Learn about bind variable syntax.
* About Using Bind Variables in Regions Based on a SQL Query or LOV
  Learn about using bind variables in regions defined as a SQL Query, SQL Query (plsql function body returning SQL query), or list of values (LOV).
* About Using Bind Variables in Regions Based on PL/SQL
  Learn about using bind variables in regions based on PL/SQL.

#### About Using Bind Variable Syntax

Learn about bind variable syntax.

In the following example, the search string is a page item.

```sql
SELECT * FROM employees WHERE last_name like '%' || :SEARCH_STRING || '%'
```

If the region type is defined as SQL Query, you can reference the value using standard SQL bind variable syntax. Using bind variables ensures that parsed representations of SQL queries are reused by the database, optimizing memory usage by the server.

When using bind variable syntax, remember the following rules:

* Bind variable names must correspond to an item name.
* Bind variable names are not case-sensitive.
* Bind variable names cannot be longer than 30 characters (that is,
  they must be a valid Oracle identifier).

  Although page item and application item names can be up to 255
  characters, if you intend to use an application item within SQL using bind
  variable syntax, the item name must be 30 characters or less.
* The data type of bind variables is always `VARCHAR2`. When a bind
  variable semantically contains a datetime or numeric value, you must perform an
  explicit conversion to the appropriate data type. For example:

  ```sql
  SELECT * FROM employees WHERE start_date < to_date(:DATE_STRING, 'DD-MON-YYYY')
  ```

#### About Using Bind Variables in Regions Based on a SQL Query or LOV

Learn about using bind variables in regions defined as a SQL Query, SQL Query (plsql
function body returning SQL query), or list of values (LOV).

If your region type is defined as a SQL Query, SQL Query (plsql function body returning SQL query), or list of values (LOV), you can reference session state using the following syntax:

```sql
:MY_ITEM
```

One common way to do this is to incorporate a session state variable in a `WHERE` clause. The following example shows how to bind the value of the item `THE_DEPTNO` into a region defined from a SQL Query.

```sql
SELECT last_name, job_id, salary
FROM employees
WHERE department_id = :THE_DEPTNO
```

See Also:

About Regions for information about creating regions

#### About Using Bind Variables in Regions Based on PL/SQL

Learn about using bind variables in regions based on PL/SQL.

For region types, processes, computations, validations, conditions, and so on that are defined as PL/SQL dynamic content, regions are constructed using PL/SQL anonymous block syntax. In other words, the beginning and ending keywords are used to enclose the PL/SQL block. For example:

```sql
IF :P1_JOB IS NOT NULL THEN
  INSERT INTO employees (employee_id, first_name, job_id)
  VALUES (:P1_EMP_ID, :P1_NAME, :P1_JOB)
end if;
```

In this example, the values of the `employee_id`, `first_name`, and `job_id` are populated by the values of `P1_EMP_ID`, `P1_NAME`, and `P1_JOB`.

### About Session Cloning

Use session cloning to open a new browser window in an Oracle APEX application and have it generate a new distinct session identifier and copy the session values from the original APEX session to the new one.

In previous releases, opening multiple windows (or browser tabs) in the same APEX application resulted in a number of issues. Typically, all the browser tabs shared
the same session and session state which resulted in unpredictable and undesirable
results.

To use session cloning, the developer must provide a method for end user to open a new browser tab and specify the `REQUEST` value of `APEX_CLONE_SESSION`. The following is an example URL:

`f?p=&APP_ID.:&APP_PAGE_ID.:&APP_SESSION.:APEX_CLONE_SESSION`

Best Practices When Using Session Cloning

When using this session cloning, developers should remember:

* The idle time associated with the Oracle APEX session would be affected by any of the APEX sessions, original or cloned ones.
* When a user logs out of one session (original or cloned), all other associated sessions will be logged out.
* The maximum session duration would be a function of the original APEX session and when it was created.
* An administrative user can enable or disable this feature using the procedure:

  ```sql
  apex_instance_admin.set_parameter(
      p_parameter => 'CLONE_SESSION_ENABLED',
      p_value     => 'Y');
  ```

See Also:

Oracle APEX API
Reference

---

<!-- fonte: htmdb/about-session-state-and-security.html -->
## About Session State and Security

Learn about managing session state and security.

Oracle APEX persists session state in database tables. Session state is preserved in database tables because it is more secure to store the session state on the server side than on the client. Because APEX applications use the stateless HTTP protocol, an application's session state across multiple page views is preserved in database tables. Not maintaining a synchronous database connection for each APEX application user significantly lessens memory and database resource requirements.

Developers can query the session state stored by APEX applications using the App Builder and built-in monitoring pages. Developers and administrators can access session state for any application in the workspace to which they are authenticated.

Developer best practices for managing session state include:

* As a standard part of implementing program control flow, clear the session state of unneeded values using clear-cache page processes or clear-cache directives in URLs used to navigate to pages.
* Use password page item types that do not save state. This prevents the entered passwords from being saved in session state tables in the database.
* When sensitive data must persist in a session, it should be saved in APEX session state tables in encrypted form. To use this feature, set the page item's Store value encrypted in session state attribute to On. Encrypted stored values are automatically decrypted when read.

Note:

The objective of encrypted session state is to persist session state such that the unencrypted values cannot be read by other APEX developers or database administrators who might have access to the APEX session state tables, debug output, or database data files. Oracle recommends that database backups be performed using facilities that encrypt data in the backup files.

Tip:

You can encrypt item values up to 4000 bytes in length. Attempts to encrypt values longer than 4000 bytes produces an error message.

---

<!-- fonte: htmdb/reviewing-session-state.html -->
## Reviewing Session State

View current session state for your application by clicking the Session link on the Runtime Developer Toolbar.

Session state enables developers to store and retrieve values for a user as the user
navigates between different application pages. The appearance or behavior of many
applications is based on data contained within application controls. For example,
buttons can display conditionally based on a value stored in session state.

See Also:

* Runtime Developer Toolbar
* Viewing Session State
* Managing Session State Values
* Managing Session State for a Workspace and Managing Session State for an Instance in Oracle APEX
  Administration Guide

---

<!-- fonte: htmdb/understanding-page-items.html -->
## Understanding Page Items

An item is part of an HTML form such as a checkbox, date picker, file browse
field, popup list of values (LOV), select list, shuttle, flip toggle switch, text field,
text area, and so on.

When defining an item, developers must follow defined naming conventions and follow specific rules when referencing item values stored in session state.

* About the Differences Between Page Items and Application Items
  Page items are placed on a page and have associated user interface properties and Application items are not associated with a page.
* About Item Naming Conventions
  When creating an item name, developers must follow very specific item naming conventions.
* Referencing Item Values
  You can reference item values stored in session state in regions, computations, processes, validation, and branches.
* About Referencing Items Using JavaScript
  When you reference an item, the best approach is to reference by ID.
* Working with Multiple Select List Item
  Learn how to handle values returned from a multiple select list item.

See Also:

About Item Types

### About the Differences Between Page Items and Application Items

Page items are placed on a page and have associated user interface properties and Application items are not associated with a page.

There are two types of items: page items and application items. Page items
are placed on a page and have associated user interface
properties, such as Display Only, Label and Label Template.
Examples of page items include a checkbox, date picker, display
as text, file browse field, popup list of values, select list,
or a text area. In contrast Application items are not
associated with a page and therefore have no user interface
properties. You can use an application item as a global
variable.

See Also:

Managing Application Items

### About Item Naming Conventions

When creating an item name, developers must follow very specific item naming conventions.

When specifying an item name, remember the following rules. Item names must:

* Be unique within an application.
* Not include quotation marks.
* Begin with a letter or a number, and subsequent characters can be letters, numbers, or underscore characters.
* Be case-insensitive.
* Should not exceed 30 characters. Items longer than 30 characters cannot be referenced using bind variable syntax. See Referencing Session State Using Bind Variable Syntax.
* Cannot contain letters outside the base ASCII character set.

As a best practice Oracle recommends including the page number when naming items. By default, wizards prefix page item names with `P``<page no>``_``<item name>` (for example, `P1_NAME)`.

### Referencing Item Values

You can reference item values stored in session state in regions, computations, processes, validation, and branches.

The following table describes the supported syntax for referencing item values.

| Type | Syntax | Description |
| --- | --- | --- |
| SQL | `:MY_ITEM` | Standard bind variable syntax for items whose names are no longer than 30 bytes. Use this syntax for references within a SQL query and within PL/SQL code. |
| PL/SQL | `V('MY_ITEM')` | PL/SQL syntax referencing the item value using the `V` function. Use this syntax in PL/SQL code of packages or stored procedures and functions.  Avoid this syntax in SQL statements. It may result in performance problems. |
| PL/SQL | `NV('MY_NUMERIC_ITEM')` | Standard PL/SQL syntax referencing the numeric item value using the `NV` function. Use this syntax in PL/SQL code of packages or stored procedures and functions.  Avoid this syntax in SQL statements. It may result in performance problems. |
| Static Text (exact) | `&MY_ITEM.` | Static text. Exact Substitution.  Note: Exact substitution syntax should be avoided in SQL or PL/SQL code because it can result in SQL Injection vulnerabilities. |

You can set the value of an item in your application using any of the following methods:

* For page items, use the Source Attribute to set the item value.

  From the page, select the item name to view the Edit Page Item page. Scroll down to Source and edit the appropriate fields.

  You can also set the value of an item in any region based on PL/SQL or a process using the following syntax:

  ```sql
  BEGIN
   :MY_ITEM :=  'new value';
  END;
  ```
* Pass the value on a URL reference using `f?p` syntax. For example:

  ```sql
  f?p=100:101:10636547268728380919::NO::MY_ITEM:ABC
  ```
* Set the value using a computation. Computations are designed to set item values. For example:

  ```sql
  TO_CHAR(SYSDATE,'Day DD Month, YYYY');
  ```
* Use the PL/SQL API to set an item value within a PL/SQL context. For example:

  ```sql
  APEX_UTIL.SET_SESSION_STATE('MY_ITEM',SYSDATE);
  ```

See Also:

* Clearing Session State
* Understanding Cross-Site Scripting Protection
* Managing Session State Values

### About Referencing Items Using JavaScript

When you reference an item, the best approach is to reference by ID.

If you view the HTML source of an Oracle APEX page in a web browser, you would notice that all items have an id attribute. This ID corresponds to the name of the item, not the item label. For example, if you create an item with the name `P1_FIRST_NAME` and a label of `First Name`, the ID is `P1_FIRST_NAME`.

You can get and set item attributes and values using the JavaScript functions `$v('P1_FIRST_NAME')` and `$s('P1_FIRST_NAME', 'Joe');`. Consider the following example:

```sql
function showFirstName(){
  alert('First Name is ' +$v('P1_FIRST_NAME'))
};
function setFirstName(pFirstName){
  $s('P1_FIRST_NAME', pFirstName);
};
```

These functions can be called by other JavaScript functions or with the Execute JavaScript code dynamic action.

See Also:

APEX_JAVASCRIPT in Oracle APEX API
Reference

### Working with Multiple Select List Item

Learn how to handle values returned from a multiple select list item.

* About Handling Values Returned from a Multiple Select List Item
  Learn about handling values returned from a multiple select list item.
* Using APEX_UTIL.STRING_TO_TABLE to Convert Selected Values
  Learn about using `APEX_UTIL.STRING_TO_TABLE` to convert selected values.

#### About Handling Values Returned from a Multiple Select List Item

Learn about handling values returned from a multiple select list item.

A multiple select item renders as a multiple select list form element which can be either a Multiselect List or Shuttle item type. When submitted, selected values are returned in a single colon-delimited string. You can handle values in this format in three ways:

* Using the `INSTR` function
* Using the `APEX_STRING.SPLIT` function
* Creating a shuttle

#### Using APEX_UTIL.STRING_TO_TABLE to Convert Selected Values

Learn about using `APEX_UTIL.STRING_TO_TABLE` to convert selected
values.

Suppose you had a report on the `EMP` and `DEPT` tables that is limited by the departments selected from a Department multiple select list. First, you create the multiple select item, P1_DEPTNO, using the following query:

```sql
SELECT dname, deptno
FROM dept
```

Second, you return only those employees within the selected departments as follows:

```sql
SELECT ename, job, sal, comm, dname
FROM emp e, dept d
WHERE d.deptno = e.deptno
AND instr(':'||:P1_DEPTNO||':',':'||e.deptno||':') > 0
```

Next, assume you want to programmatically step through the values selected in the multiple select item, P1_DEPTNO. To accomplish this task, convert the colon-delimited string into a PL/SQL array using the `apex_string.split` function. The following example demonstrates how to insert the selected departments into an audit table containing the date of the query.

```sql
DECLARE
  l_selected apex_t_varchar2;
BEGIN
  --
  -- Convert the colon separated string of values into
  -- a PL/SQL array
  l_selected := apex_string.split(
                    p_str => :P1_DEPTNO,
                    p_sep => ':' );

  --
  -- Loop over array to insert department numbers and sysdate
  --

  FOR i IN 1..l_selected.count
  LOOP
    INSERT INTO report_audit_table (report_date, selected_department)
        VALUES (sysdate, l_selected(i));
  END LOOP;
END;
```

See Also:

STRING_TO_TABLE Function in Oracle APEX API
Reference

---

<!-- fonte: htmdb/managing-page-items.html -->
## Managing Page Items

View existing page items, create new page items, and edit an item to change
its appearance or behavior.

Tip:

See About Item Types to learn more about the item types available in App Builder.

* Understanding Page Items
  An item is part of an HTML form such as a checkbox, date picker, file browse field, popup list of values (LOV), select list, shuttle, flip toggle switch, text field, text area, and so on.
* Viewing Page Items
  Configure page items to control how items display.
* Creating Page Items
  Create page items in Page Designer in either the Rendering tab or by adding an item from the Gallery.
* Editing Page Items
  Edit item attributes to control how an item displays on a page.

---

<!-- fonte: htmdb/creating-page-items.html -->
## Creating Page Items

Create page items in Page Designer in either the Rendering tab or by adding
an item from the Gallery.

* Creating a Page Item from the Rendering Tab
  Create a page item in Page Designer from the Rendering tab.
* Adding a Page Item from the Gallery
  Create a page item in Page Designer by adding it from the Gallery.
* Creating a Static List of Values
  Create a static list of values locally with the definition of the item.
* Creating a Cascading List of Values
  Create a cascading list of values locally with the definition of the item.
* Creating a Shuttle Item on the Form Page
  Create a shuttle item in Page Designer.

---

<!-- fonte: htmdb/editing-page-items.html -->
## Editing Page Items

Edit item attributes to control how an item displays on a page.

For example, the Type attribute determines if the item displays as text field, text
area, checkbox, date picker, switch, hidden item and so on.
Depending upon the item Type, item attributes can determine
where a label displays, how large an item is, and if the item
displays next to or below the previous item. Item attributes
also control item behavior such as the item’s default value,
whether the item displays conditionally, or if the item is
read-only.

* Editing Page Item Attributes in the Property Editor
  Learn about editing page item attributes in the Property Editor.
* Positioning Page Items
  Position page items at a page or region level.
* Defining Default Values for Page Items
  Define default values for an item using the Default attribute.
* Configuring Page Item Security
  Learn about editing page item Security attributes in the Property Editor.
* Changing an Existing Item to Use Quick Picks
  Change an item to use a quick picks list by edting the Quick Picks attributes in Page Designer.
* Configuring Multiple Value Attributes
  Control how lists are stored or define custom separators using Multiple Value attributes.
* Displaying Conditional Page Items
  Display an item conditionally by editing Server-side Condition attributes.
* Displaying Read Only Page Items
  Display a read-only item by editing the Read Only attribute in Page Designer.
* Applying a Format Mask to an Item
  Apply a format mask to an item by editing the Format Mask attribute.
* Configuring Item Attributes to Warn Users of Unsaved Changes
  Configure the Warn on Unsaved Changes attribute to specify if the page item should be included in the unsaved changes check.
* Controlling How Page Items Write Session State
  Control how a page item maintains session state by configuring the Session State, Storage attribute.
* Viewing Item Utilities
  Access the Utilities page to view Grid Edit pages and reports that enable you to edit items on multiple pages within a selected application.

### Editing Page Item Attributes in the Property Editor

Learn about editing page item attributes in the Property Editor.

To edit item attributes in the Property Editor:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays the Page Item attributes. Attributes
   are organized in groups. To search for a group or an attribute, enter a
   keyword in the Filter Properties field. The Property Editor displays the
   group or attributes. Or, you can click Go to Group
   and select the group.
3. Edit the appropriate attributes in the Property Editor.

   Edited attributes display a green marker to the left of the attribute name
   until the page is saved.

   To learn more about an attribute, select the attribute in the
   Property Editor and click the Help tab in the central
   pane.
4. To save your changes click Save. To save and run the
   page, click Save and Run Page.

### Positioning Page Items

Position page items at a page or region level.

To position a page item at the page-level:

1. Select the page item in Page Designer.
2. In the Property Editor leave the Layout,
   Region attribute empty.
3. To place a page item at a specific location on the page, configure the
   Layout, Position
   attribute.

To position a page item at a region-level:

1. Select the page item in Page Designer.
2. In the Property Editor, edit the Layout,
   Region attribute and select the region where the page
   item belongs.
3. Configure the Layout, Position
   within the region to place a Page Item at a specific location inside the
   region.

### Defining Default Values for Page Items

Define default values for an item using the Default attribute.

The default value is used when the item's value is not derived from session
state and when the source value is `NULL`.

To define a default value for an item:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays the Page Item attributes. Attributes
   are organized in groups. To search for a group or an attribute, enter a
   keyword in the Filter Properties field. The Property Editor displays the
   group or attributes. Or, you can click Go to Group
   and select the group.
3. In the Property Editor, find the Default group.
4. Default, Type - Select a default value type for this item. Options
   include:
   * Static - Set to the value entered in
     Static Value.
   * Item - Set to the value returned from
     the session state for the selected Item.
   * SQL Query - Set to the value returned
     from the entered SQL Query.
   * SQL Query returning Colon Delimited
     List - Set to the colon delimited list of values returned
     from the entered SQL Query . Colon delimited lists are required when the
     column is displayed as a checkbox, radio group, or shuttle.
   * PL/SQL Expression - Set to the value
     returned from the entered PL/SQL Expression.
   * PL/SQL Function Body - Set to the
     value returned from the PL/SQL Function Body entered.
   * Sequence - Set to the value returned
     from the Sequence entered.
5. To save your changes click Save. To save and run the
   page, click Save and Run Page.

### Configuring Page Item Security

Learn about editing page item Security attributes in the Property
Editor.

To configure page item security:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays the item attributes.
   Attributes are organized in groups. To find a group or attribute, enter keywords in the
   Filter Properties field, or click Go to Group and select the
   group.
3. Under Security:

   * Security, Authorization Scheme - Select an authorization scheme to
     control this component. The authorization must evaluate to TRUE in order for this
     component to be rendered or executed.

     See Also:
     Providing Security Through Authorization
   * Security, Session State Protection level - Select a Session State
     Protection level. Options include:

     + Unrestricted - The item can be set by
       passing the item in a URL or in a form. No checksum is required in the URL.
     + Checksum Required - Application Level - The
       item can be set by passing the item in a URL that includes a checksum specific
       to the workspace and application.
     + Checksum Required - User Level - The item
       can be set by passing the item in a URL that includes a checksum specific to the
       workspace, application and user.
     + Checksum Required - Session Level - The
       item can be set by passing the item in a URL that includes a checksum specific
       to the session.
     + Restricted - May not be set from browser -
       The item cannot be altered using the URL or POSTDATA. Select this option to
       restrict what can set the item value to internal processes, computations, and so
       on. This attribute only applies to items that are not used as data entry items
       and is always observed, even if Session State Protection is disabled. Use this
       attribute for page or application items that have the following Display As
       types

       - Display Only (Save State=No)
       - Text Field (Disabled, does not save state)

     See Also: Preventing URL Tampering
   * Security, Store value encrypted in session state - Specify whether to
     encrypt this item when stored in session state. If the contents of an item contains
     sensitive data, then you should encrypt the value when it is stored in the Oracle APEX session state management tables. Otherwise, anyone with rights to read the Oracle APEX meta data tables could potentially write a query to extract this sensitive
     data.

     See Also: Understanding Cross-Site Scripting Protection
   * Security, Restricted Characters - Select how to restrict the characters
     that can be saved in session state. APEX displays an error message if a user tries to save data that does not conform to
     the selected character restriction. Restricting the characters hardens application
     security and is a possible counter measure to cross-site scripting (XSS) attacks.

     Available options include:

     + All characters can be saved - No restriction applies.
     + Allowlist for a-Z, 0-9 and space - Only allow characters
       a-z, A-Z, 0-9, and space.
     + Blocklist HTML command characters (<>") - Reserved
       HTML characters cannot be saved.
     + Blocklist &<>"/;,\*|=% and --: - The following
       characters cannot be saved:

       &, <, >, ", /, ;, ",", \*, |, =, % and "--" (PL/SQL
       comment)
     + Blocklist &<>"/;,\*|=% or -- and new line - The
       following characters cannot be saved:

       &, <, >, ", /, ;, ",", \*, |, =, %, "--", and new line
       characters
4. To save your changes click Save. To save and run the page, click
   Save and Run Page.

### Changing an Existing Item to Use Quick Picks

Change an item to use a quick picks list by edting the Quick Picks attributes in
Page Designer.

Quick picks enable users to select predefined values with just one click, rather than typing in text or selecting from a list of available options. If the item type supports quick pick selection, use the Quick Picks attributes to define up to ten selections that display under a give item. Clicking on a quick pick sets the value of item. The following example shows quick picks for 5%, 10%, 15%, and 20%.

To create a quick pick:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays the item attributes. Attributes
   are organized in groups. To find a group or attribute, enter keywords in the
   Filter Properties field, or click Go to Group and select
   the group.
3. Under Quick Picks:
   1. Quick Picks, Show Quick Picks - Select On
      .
   2. Quick Picks, Link Attributes - Enter HTML attributes that are
      associated with the display of each Quick Pick link
   3. Quick Picks, Label - Enter the label for the each Quick Pick. This
      label is the text the end user of the application sees.
   4. Quick Picks, Value - Enter the value associated with each Quick Pick.
      This value replaces the existing item value when the user clicks the
      quick pick.
   5. Repeat the previous two steps until all Quick Pick labels and values
      have been defined.
4. To save your changes click Save. To save and run the
   page, click Save and Run Page.

### Configuring Multiple Value Attributes

Control how lists are stored or define custom separators using Multiple
Value attributes.

You can configure Multiple Values
attributes for the folowing item types: Checkbox Group, Combobox, List Manager,
Popup LOV, Select List, Select Many, and Shuttle. Configuration of these attributes
is required for Checkbox Group, List Manager, Select Many, and Shuttle.

these

The Multiple Values group contain two attributes.
Type determines whether the Source Column contains
multiple values and how these are encoded. Separator enables
you to define the character which separates values from one other.

To edit Multiple Values attributes:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays the item attributes. Attributes
   are organized in groups. To find a group or attribute, enter keywords in the
   Filter Properties field, or click Go to Group and select
   the group.
3. Under Multiple Values:
   1. Multiple Values, Type - Determines whether the Source Column contains
      multiple values and how these are encoded.

      Options include:

      * No - Column does not
        contain multiple values.
      * Delimited List - Column
        contains values as a delimited list. Example:

        `APEX,SQL,PL/SQL`

        Use the `APEX_STRING.SPLIT`
        function for processing, for example:

        ```sql
        select column_value from apex_string.split ( :ITEM_NAME, ',' );
        ```
      * JSON Array - The Source
        column contains a JSON array of scalar values. If the column
        contains invalid JSON syntax, APEX will raise error messages, for example:

        ```sql
        ["APEX", "SQL", "PL/SQL"]
        ```

        Use the `JSON_TABLE SQL` function
        for processing, for example:

        ```sql
        select
            element
        from
            json_table ( :ITEM_NAME, '$[*]'
                columns
                    element varchar2 path '$'
            );
        ```
   2. Multiple Values, Separator - Identifies the character which separates
      values from one other. To view examples, see Page Designer Help.

      Note:

      Double-quote ("),
      backslash (/) characters or characters in the `\xxxx`
      format are not supported as a Value Separator.
4. To save your changes click Save.

### Displaying Conditional Page Items

Display an item conditionally by editing Server-side Condition attributes.

To display a conditional item:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays Page Item attributes. Attributes are
   organized in groups.

   To find a group or attribute, enter keywords in the Filter field. The
   Property Editor displays the group or attributes. Or, you can click Go to
   Group and select the group.
3. Server-side Condition, Type - Select a condition type that must be met in order for
   this component to be rendered or processed.

   To learn more about an attribute, select the attribute in the Property
   Editor and click the Help tab in the central pane.
4. To save your changes click
   Save. To save and run the
   page, click Save and Run
   Page.

### Displaying Read Only Page Items

Display a read-only item by editing the Read Only attribute in Page
Designer.

To display a read-only item:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays attributes for the item. Attributes are
   organized in groups. To find a group or attribute, enter keywords in the Filter Properties
   field, or click Go to Group and select the group.
3. Under Read Only:
   1. Read Only, Type - Select a condition type that must be met in order for this
      component to render as read-only.

      Not selecting a condition causes the item to render normally. A
      read-only item is rendered with the same settings as a Display Only item.

      To always render the item as an enterable field, set the condition type
      to Never. This setting overwrites any read-only condition
      setting on the region or page level.
   2. The UI may change depending on the Type you select. Edit the appropriate
      attributes.

      To learn more, select the attribute in the Property Editor and click
      the Help tab in the central pane
4. To save your changes click Save. To save and run the page, click
   Save and Run Page.

### Applying a Format Mask to an Item

Apply a format mask to an item by editing the Format Mask attribute.

Developers commonly select a format mask to determine how numbers and dates
display.

To apply a format mask to an item:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays Page Item attributes. Attributes are
   organized in groups.

   To find a group or attribute, enter keywords in the Filter field. The
   Property Editor displays the group or attributes. Or, you can click Go to
   Group and select the group.
3. Appearance, Format Mask - Select a format mask.

   Tip:

   Only apply number format
   masks to items that contain numbers and only apply date format masks to items that
   contain dates. Otherwise, is raised since the component contains a value that can not be
   converted using the specified format mask.
4. To save your changes click
   Save. To save and run the
   page, click Save and Run
   Page.

### Configuring Item Attributes to Warn Users of Unsaved Changes

Configure the Warn on Unsaved Changes attribute to specify if the page item should be
included in the unsaved changes check.

Developers can use the Warn on Unsaved Changes item attribute
to specify if the page item should be included in the unsaved changes check. This
check warns the user when they try to navigate away from a page and when the page
contains unsaved changes. Items not based on a database column (for example, a
search item) may not need to be checked. For those items, set Warn on
Unsaved Changes to Do Not Check.

To configure the Warn on Unsaved Changes attribute:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays Page Item attributes. Attributes
   are organized in groups.

   To find a group or attribute, enter keywords in the Filter
   field. The Property Editor displays the group or attributes. Or, you can
   click Go to Group and select the group.
3. Advanced, Warn on Unsaved Changes - Select one of the following:

   * Page Default - Include item in the
     unsaved changes check if Warn on Unsaved
     Changes is enabled at the page-level.
   * Ignore - Changes to the item are
     ignored by the unsaved changes check. Select this option for items
     not based on a database column (for example, a search item).
4. To save your changes click Save. To save and run the page, click
   Save and Run Page.

Tip:

The
Warn on Unsaved Changes attribute is implemented using
the `apex.page.warnOnUnsavedChanges` API.

See Also:

* Configuring Pages to Warn Users of Unsaved Changes
* warnOnUnsavedChanges in Oracle APEX JavaScript
  API Reference

### Controlling How Page Items Write Session State

Control how a page item maintains session state by configuring the Session State,
Storage attribute.

To configure page item writes session state:

1. View the page containing the item to be configured in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays the item attributes.
   Attributes are organized in groups. To find a group or attribute, enter keywords
   in the Filter Properties field, or click Go to Group and
   select the group.
3. In the Property Editor, find the Session State
   group.
4. Session State, Storage - Select how session state is maintained. Options
   include:
   * Per Request (Memory Only) - Do not
     save state in the database. State is only available when processing the
     current request. When AJAX requests need to use an item, make sure to pass
     the item name using Page Items To Submit.
   * Per Session (Disk)- Maintain for
     each session by storing the value in the database, to access it across
     requests.
   * Per User (Disk) - Maintain for a user
     by storing the value in the database, to access it across sessions.

   Note:

   When creating database
   items that work with a Form region (for example as part of a wizard),
   Per Request (Memory Only) is the default. Per
   User (Disk) is not available for these
   items.
5. To save your changes click Save. To save and run the
   page, click Save and Run Page.

See Also:

About Setting Session State

### Viewing Item Utilities

Access the Utilities page to view Grid Edit pages and reports that enable you to edit
items on multiple pages within a selected application.

To access the Utilities page:

1. On the Workspace home page, click the App
   Builder icon.
2. Select an application.
3. Click Utilities.
4. From Page Specific Utilities region, click Item Utilities.
5. Select one of the following reports:

   * Edit Item Help
     Text - Edit item help text to ensure consistency across your
     application.
   * All Page
     Items - Edit all page items in your
     application.
   * Password
     Items - Edit password items in your
     application. Oracle recommends password items not
     save session state. To learn more, see the
     Password Items region on
     the right side of the page.
   * Conditional
     Items - Edit conditional items in your
     application.

---

<!-- fonte: htmdb/viewing-page-items.html -->
## Viewing Page Items

Configure page items to control how items display.

To view page attributes in Page Designer:

1. View the page in Page Designer:
   1. On the Workspace home page, click the App
      Builder icon.
   2. Select an application.
   3. Select a page.

   Page Designer appears.
2. In either the Rendering tab or the Layout tab, select the item to edit.

   The Property Editor displays Page Item attributes. Attributes
   are organized in groups.

   To find a group or attribute, enter keywords in the Filter
   field. The Property Editor displays the group or attributes. Or, you can
   click Go to Group and select the group.
3. Edit the appropriate attributes in the Property Editor.

   Edited attributes display a green marker to the left of the
   attribute name until the page is saved.

   To learn more about an attribute, select the attribute in the
   Property Editor and click the Help tab in the central
   pane.
4. To save your changes click Save. To save and run the
   page, click Save and Run Page.

Tip:

See About Item Types to learn more about the item types available in App Builder.
