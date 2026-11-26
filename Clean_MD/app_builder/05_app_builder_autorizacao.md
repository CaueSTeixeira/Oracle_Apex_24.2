# 05_app_builder_autorizacao
Fonte: Oracle APEX 24.2 App Builder User's Guide — https://docs.oracle.com/en/database/oracle/apex/24.2/htmdb/

<!-- fonte: htmdb/how-authorization-schemes-work.html -->
## How Authorization Schemes Work

Learn about how an authorization scheme extends the security of your application's authentication scheme.

You can specify an authorization scheme for an entire application, page, or specific control such as a region, item, or button. For example, you could use an authorization scheme to selectively determine which tabs, regions, or navigation bars a user sees. An authorization scheme either succeeds or fails. Common authorization scheme types include Exists, Not Exists SQL Queries, and PL/SQL Function Returning Boolean. If a component or control level authorization scheme succeeds, the user can view the component or control. If it fails, the user cannot view the component or control. If an application or page-level authorization scheme fails, then Oracle APEX displays a previously defined message.

When you define an authorization scheme, you give it a unique name. Once defined, you can attach it to any component or control in your application. To attach an authorization scheme to a component or control in your application, simply navigate to the appropriate attributes page and select an authorization scheme from the Authorization Scheme list.

---

<!-- fonte: htmdb/about-authorization-scheme-types.html -->
## About Authorization Scheme Types

Select an authorization scheme type when you create an authorization
scheme.

The authorization scheme type determines how an authorization scheme is applied.
Developers can create new authorization type plug-ins to extend this list.

| Authorization Scheme Types | Description |
| --- | --- |
| Exists SQL Query | Enter a query that causes the authorization scheme to pass if it returns at least one row and causes the scheme to fail if it returns no rows |
| NOT Exists SQL Query | Enter a query that causes the authorization scheme to pass if it returns no rows and causes the scheme to fail if it returns one or more rows |
| PL/SQL Function Returning Boolean | Enter a function body. If the function returns true, the authorization succeeds. |
| Item in Expression 1 is NULL | Enter an item name. If the item is null, the authorization succeeds. |
| Item in Expression 1 is NOT NULL | Enter an item name. If the item is not null, the authorization succeeds. |
| Value of Item in Expression 1 Equals Expression 2 | Enter and item name and value. The authorization succeeds if the item's value equals the authorization value. |
| Value of Item in Expression 1 Does NOT Equal Expression 2 | Enter an item name and a value. The authorization succeeds if the item's value is not equal to the authorization value. |
| Value of Preference in Expression 1 Does NOT Equal Expression 2 | Enter an preference name and a value. The authorization succeeds if the preference's value is not equal to the authorization value. |
| Value of Preference in Expression 1 Equals Expression 2 | Enter an preference name and a value. The authorization succeeds if the preference's value equal the authorization value. |
| Is In Group | Enter a group name. The authorization succeeds if the group is enabled as a dynamic group for the session. See APEX_AUTHORIZATION.ENABLE_DYNAMIC_GROUPS in Oracle APEX API Reference.  If the application uses APEX Accounts Authentication, this check also includes workspace groups that are granted to the user. If the application uses Database Authentication, this check also includes database roles that are granted to the user. |
| Is Not In Group | Enter a group name. The authorization succeeds if the group is not enabled as a dynamic group for the session. |

---

<!-- fonte: htmdb/creating-an-authorization-scheme.html -->
## Creating an Authorization Scheme

Create an authorization scheme on the Shared Components page.

To create an authorization scheme:

1. On the Workspace home page, click the App
   Builder icon.
2. Select an application.
3. On the Application home page, click Shared Components.

   The Shared Components page appears.
4. Under Security, select Authorization Schemes.
5. Click Create.
6. Specify how to create an authorization scheme by selecting one of the following:
   * From Scratch
   * As a Copy of an Existing Authorization Scheme
7. On Create Authorization Scheme - Details:

   1. Name - Enter an unique name that identifies this authorization scheme.
   2. Scheme Type - Select how this authorization scheme will be applied. See About Authorization Scheme Types.
   3. Identify error message displayed when scheme violated - Enter error text that displays if the authorization scheme fails (that is, the current user fails the security check).
   4. Validate Authorization Scheme - Authorization schemes are evaluated on first use in a session. Use this option to controls if future uses cause re-evaluations and when a memorized result can be taken instead.

   For more details, see field-level Help.
8. Click Create Authorization Scheme.

See Also:

* Attaching an Authorization Scheme to an Application, Page, or Components
* Changing the Evaluation Point Attribute
* About Resetting Authorization Scheme State

---

<!-- fonte: htmdb/attaching-an-authorization-scheme.html -->
## Attaching an Authorization Scheme to an Application, Page, or Components

Attach an authorization scheme to an entire application, page, control, or
component.

Tip:

Before you can attach an authorization scheme to an application, page,
control, or component, you must first create it. See Creating an Authorization Scheme.

* Attaching an Authorization Scheme to an Application
  Learn how to attach an authorization scheme to an application.
* Attaching an Authorization Scheme to a Page
  Learn how to attach an authorization scheme to a page.
* Attaching an Authorization Scheme to a Control or Component
  Learn how to attach an authorization scheme to a control or component.

### Attaching an Authorization Scheme to an Application

Learn how to attach an authorization scheme to an application.

To attach an authorization scheme to an application:

1. On the Workspace home page, click the App Builder icon.
2. Select an application.
3. Click the Shared Components icon.

   The Shared Components page appears.
4. Under Security, click Security Attributes.
5. Scroll down to Authorization and make a selection from the Authorization Scheme list.
6. For Run on Public Pages, select On or Off to specify whether the application-level authorization scheme is checked on public pages (that is, pages that do not require authorization). To learn more, see Authorization.
7. To define a new authorization scheme, click Define Authorization Schemes.

### Attaching an Authorization Scheme to a Page

Learn how to attach an authorization scheme to a page.

To attach an authorization scheme to a page:

1. On the Workspace home page, click the App
   Builder icon.
2. Select an application.
3. Select a page.

   Page Designer appears.
4. In the Rendering tab on the left side, click the page title at the top of the tree.
5. In the Property Editor, locate Security and make a selection from the Authorization Scheme attribute.

   Tip:

   To find a group or attribute:

   * Search for the group or attribute - Enter keywords in the Filter Properties field. The Property Editor displays the group or attributes. To return to the default display, delete the keywords.
   * Use Go to Group - Click Go to Group and select the group. To return the default display, click Go to Group again and select Expand All.
6. Click Save.

### Attaching an Authorization Scheme to a Control or Component

Learn how to attach an authorization scheme to a control or component.

To attach an authorization scheme to a page component or control:

1. On the Workspace home page, click the App
   Builder icon.
2. Select an application.
3. Select a page.

   Page Designer appears.
4. Select the component or control to which you want to apply the authorization scheme.
5. In the Property Editor, locate Security and make a selection from the Authorization Scheme attribute.

   Tip:

   To find a group or attribute:

   * Search for the group or attribute - Enter keywords in the Filter Properties field. The Property Editor displays the group or attributes. To return to the default display, delete the keywords.
   * Use Go to Group - Click Go to Group and select the group. To return the default display, click Go to Group again and select Expand All.
6. Click Save.

---

<!-- fonte: htmdb/providing-security-through-authorization.html -->
## Providing Security Through Authorization

Extend the security of your application by creating an authorization scheme.

Authorization is a broad term for controlling access to resources based on user privileges. While conditions control the rendering and processing of specific page controls or components, authorization schemes control user access to specific controls or components.

* How Authorization Schemes Work
  Learn about how an authorization scheme extends the security of your application's authentication scheme.
* About Authorization Scheme Types
  Select an authorization scheme type when you create an authorization scheme.
* Creating an Authorization Scheme
  Create an authorization scheme on the Shared Components page.
* Attaching an Authorization Scheme to an Application, Page, or Components
  Attach an authorization scheme to an entire application, page, control, or component.
* Editing an Authorization Scheme
  Learn how to edit an authorization scheme.
* Copying or Subscribing to an Authorization Scheme
  Copy an authorization scheme from the current application or from another applications. When copying an authorization scheme from another app, you can also subscribe to it.
* Viewing Authorization Reports
  View the Authorization Scheme Subscription and Authorization Scheme Utilization reports to better manage authorization schemes within your application.
