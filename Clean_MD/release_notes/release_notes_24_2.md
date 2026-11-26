# Release Notes APEX 24.2 (novidades, mudanças, deprecados, problemas conhecidos)
Fonte: https://docs.oracle.com/en/database/oracle/apex/24.2/htmrn/

<!-- fonte: htmrn/new-features.html -->
## 2 New Features

Oracle APEX release 24.2 includes a number of new features. These new features are not present in APEX release 24.1 and earlier releases.

* JSON Sources
* JSON Duality Views
* Vector Search
* REST Source Enhancements
* Workflow Enhancements
* Database Object Dependencies
* Shared Component Utilization Reports
* Support for Fusion Integration
* BOSS REST Service Support
* Document Generator Enhancements
* Dynamic Action: Generate Text with AI
* Create Custom Data Models Using AI
* AI Configurations and RAG Sources
* Control Breaks for Template Components
* Unlimited Attributes for Item Plug-ins
* Export App Enhancements
* Default RTL Direction Based on Language
* Builder Extension Auto-Subscribe
* Text Messages Enhancements
* New Substitution String
* Application User Experience Data (OpenTelemetry)
* Generative AI Configuration Screen Enhancements
* Improved Content-Security-Policy Support
* Improved Popup LOV Functionality
* Accessibility Improvements
* Theme Metadata Decoupled from Application Metadata
* Select Many Improvements
* Universal Theme Enhancements
* PL/SQL API Updates
* JavaScript API Updates
* JavaScript Library Upgrades

### 2.1 JSON Sources

JSON Sources in APEX consist of information about the owner and name of a database table. You can use a plain table with columns containing JSON data or a JSON collection table. After picking the table and column to use, APEX either determines the data profile from the actual data or uses an uploaded JSON Schema file.

JSON Sources are available to page components, including reports, charts, and forms, and shared components, including lists of values and automations. For more on using JSON Sources, see Managing JSON Sources in Oracle APEX App Builder
User’s Guide.

JSON Sources are available on Oracle Database 19c and later.

### 2.2 JSON Duality Views

**JSON-relational duality** underpins collections of documents with relational storage: active, updatable, hierarchical documents based on a foundation of normalized relations. You can define a duality view using a local database or a REST Enabled SQL reference. After selecting a duality view, Oracle APEX retrieves a JSON schema from the database and builds a data profile. The data profile maps JSON attributes to columns with data types that APEX components can consume.

Duality views are available to page components, including reports, charts, and forms, and shared components, including lists of values and automations. For more on using Duality Views, see Managing Duality Views in Oracle APEX App Builder
User’s Guide.

Duality Views are available on Oracle Database 23ai or later.

### 2.3 Vector Search

Vector Search is now available for APEX instances running on Oracle
Database 23ai. Create a Search Configuration on top of a table with columns of the `VECTOR` data type, and configure details including index usage, distance metrics, maximum vector distance, or maximum results. APEX returns search results in order of vector similarity.

To configure **Oracle Vector Search**, you must set up a **Vector Provider** to convert search expressions into vectors. Vector Providers are configured at the workspace level, and available in all applications. For more information, see Managing Vector Providers in Oracle APEX App Builder
User’s Guide.

### 2.4 REST Source Enhancements

Support for Token-Based Pagination in Simple HTTP REST Data Sources

The **Simple HTTP** REST Data Source type now supports REST services with token-based pagination, enhancing integration with APIs that use this pagination scheme.

Flexible Remote Servers

When editing a remote server, you can now use placeholders (for example, `#tenant#`) within the endpoint URL as well as within other attributes. At runtime, APEX can derive the placeholder values as well as the Base URL of a Remote Server object (used for REST Data Sources, REST Enabled SQL, and Authentication) dynamically with a PL/SQL **Configuration Procedure**. This allows APEX to invoke the endpoints dynamically based on the current application, tenant, or environment settings.

For more information on flexible remote servers, see About Flexible Remote Servers in Oracle APEX App Builder
User’s Guide.

### 2.5 Workflow Enhancements

New Activity: Invoke Workflow

Use the new **Invoke Workflow** activity to invoke another workflow from a parent workflow.

You can now specify workflow parameter directions as **In**, **Out**, or **In/Out**. **Out** parameters can only be set when the workflow is used in the Invoke Workflow activity of another workflow. **Out** parameters do not show up when the workflow is used in a page process.

When adding or updating a workflow parameter, the component parameters in the workflow page process are automatically synchronized to reflect the changes. The Synchronize Parameters menu option from the Page Process is removed because the synchronization now happens automatically.

For existing workflows, you can regenerate the Workflow Details page from the Create Page wizard so that the To Parent Workflow button appears in the details of the invoked workflow.

CLOB Support for Variables and Parameters

Workflow parameters and workflow variables now support `CLOB` data types.

When a CLOB is displayed on the workflow details page, only the section of the CLOB that is accommodated within the `VARCHAR2` limit for SQL displays.

If the value of the CLOB exceeds the `VARCHAR2` limit, use `apex_workflow.update_variables` to update the variable instead of using the workflow details page.

Copy Workflow from Other Application

You can now copy a workflow from another application using Copy From Other App in Shared Components, Workflows and Automations.

When you copy a workflow, you also copy:

* the workflow versions, parameters, activities, participants, and variables
* other shared components referenced in the workflow, including email templates, tasks, and REST sources
* all invoked workflows, if they are not already present in the current application

Resume Workflow at Any Activity

Suspended workflows can now resume at any activity by using the API `APEX_WORKFLOW.RESUME`. For more information on how to configure this, including an example of how to expose relevant information in the workflow detail page, see Resuming Suspended Workflows in Oracle APEX App Builder
User’s Guide.

Support for Workflow and Human Task Runtime Instance Export

You can now export workflow and human task runtime instances when exporting an application. You can use this functionality to move instance data from one environment to another. For more information, see APEX_EXPORT.GET_APPLICATION Function in Oracle APEX API
Reference.

### 2.6 Database Object Dependencies

The new **Database Object Dependencies** report makes it easy to scan and report database object dependencies for applications in your workspace. Scan the whole application at once or one page at a time to view the dependencies, including:

* tables and table columns
* views
* packages, procedures, and functions
* links to the component property of each dependency
* system dependencies, including references to Oracle Database APIs and APEX Views

The report also contains a section for **System Dependencies**, including references to Oracle Database APIs and APEX Views. You can use the report to review application code that references any selected database object.

The new **Database Object Dependencies** report improves the `APEX_APP_OBJECT_DEPENDENCY` API introduced in APEX 24.1 with bug fixes and performance improvements. The **Database Object Dependencies** report can now detect dependencies from:

* SQL expressions in report columns
* REST Service queries (`#APEX$SOURCE_DATA#`)
* Data Profile SQL expressions

For more information on the Database Object Dependencies report, see Viewing Database Object Dependencies in Oracle APEX App Builder
User’s Guide.

### 2.7 Shared Component Utilization Reports

Shared Component utilization reports for Task Definitions, Email Templates, and REST Data Sources are now enhanced to show usage of workflows and tasks.

### 2.8 Support for Fusion Integration

You can now create an application from the Create Application Wizard with pre-configured integrations to Oracle Fusion Applications. This automates the manual steps previously necessary to set up federated authentication and identity propagation between APEX and Fusion.

Select Create Fusion Integration in the Create Application Wizard to create:

* a starter application
* a Remote Server, pre-configured to reference the base URL of your Fusion REST API endpoints
* a Web Credential for the Authentication Scheme and the sample REST Data Source
* a pre-configured Authentication Scheme
* a sample REST Data Source

For more information, see Integrating APEX with Fusion Applications in Oracle APEX App Builder
User’s Guide. You must have an OCI Database Tools Connection configured in order to see the Create Fusion Integration option.

### 2.9 BOSS REST Service Support

You can now easily use Fusion Apps REST APIs with URLs that contain `/api/boss` in any APEX region:

* Discover all supported operations and attributes during REST Data Source creation.
* Automatically delegate filtering and sorting to the BOSS service API.
* Optimize performance by only retrieving and sending attributes the current region uses.
* Work programmatically with BOSS endpoints using `APEX_EXEC`.

For more information on BOSS REST Service Support, see About Oracle Cloud Applications BOSS REST Services in Oracle APEX App Builder
User’s Guide.

### 2.10 Document Generator Enhancements

When **Document Generator** is configured as print server, you can now also upload XLSX files. **Document Generator** now supports these additional output types:

* DOCX to DOCX
* XLSX to PDF
* XLSX to XLSX

### 2.11 Dynamic Action: Generate Text with AI

You can now use the Dynamic Action **Generate Text With AI** to call the configured Generative AI Service and generate a one-time response based on user content. This action is ideal for tasks like summarizing or translating text, extracting keywords, or drafting emails. For more information on using this dynamic action, see Creating a Dynamic Action to Generate Text with AI in Oracle APEX App Builder
User’s Guide.

### 2.12 Create Custom Data Models Using AI

A new SQL Workshop utility, **Create Data Model using AI**, uses AI to help you create your own schemas. The APEX Assistant generates a script to create tables, triggers, and constraints in either Oracle SQL or Quick SQL.

Before you can use this feature, you must create a Generative AI Service and enable the Used by App Builder setting. For more information, see Creating a Data Model Using AI in Oracle APEX SQL Workshop
Guide.

### 2.13 AI Configurations and RAG Sources

**AI Configuration** is a reusable component that centralizes key Generative AI settings, including System Prompt, Welcome Message, and RAG (Retrieval-Augmented Generation) Sources, for use across AI-enabled features in APEX.

With this release, RAG Sources allow applications to dynamically add relevant data to AI responses, with flexible conditions to control inclusion based on user prompts or security settings. See Managing AI Configurations and RAG Sources in Oracle APEX App Builder
User’s Guide.

### 2.14 Control Breaks for Template Components

APEX now supports **control breaks** (grouping) for Template Component Reports. You can configure groups declaratively for Template Component Report Regions in Page Designer.

APEX also supports grouping for:

* the `APEX_EXEC` API
* Content Row template components

### 2.15 Unlimited Attributes for Item Plug-ins

In APEX 24.1, the custom attribute limit for Region plug-ins was lifted. In 24.2, this is extended to Item plug-ins as well. New item plug-ins automatically have unlimited attributes.

Modifying Existing Plug-ins

To modify existing plug-ins to have unlimited attributes:

1. Edit your item plug-in and set the API Interface attribute to `Procedure`.
2. Update your custom attributes:

   ```sql
   -- old
   l_my_attribute varchar2(32767) := p_item.attribute_01;
   l_my_number    number          := p_item.attribute_02;
   l_my_boolean   boolean         := p_item.attribute_03 = Y;

   -- new
   l_my_attribute varchar2(32767) := p_item.attributes.get_varchar2( 'attribute_01');
   l_my_number    number          := p_item.attributes.get_number  ( 'attribute_02');
   l_my_boolean   boolean         := p_item.attributes.get_boolean ( 'attribute_03', true);
   ```
3. The Substitute Attribute Values switch is deprecated. When you move to the Procedure interface, this switch disappears. To perform substitutions on the attribute values, use new parameters in the `get_varchar2` function:
   * `p_do_substitutions`
   * `p_do_serveronly_substitutions`
   * `p_substitution_escape_mode`

   ```sql
   procedure render (
       p_item   in            apex_plugin.t_item,
       p_plugin in            apex_plugin.t_plugin,
       p_param  in            apex_plugin.t_item_render_param,
       p_result in out nocopy apex_plugin.t_item_render_result )
   as
       -- Old
       l_my_attribute varchar2(32767) := p_item.attribute_01;

       -- NEW
       l_my_attribute varchar2(32767) := p_item.attributes.get_varchar2 (
                                         p_static_id                => 'my_static_id',
                                         p_do_substitution          => true,
                                         p_substitution_escape_mode => apex_session_state.c_escape_mode_html );
   begin
   ...
   ...
   end;
   ```

When upgrading to APEX 24.2, custom attributes receive the new Static ID when migrated. For example, an attribute with sequence 1 gets the ID "`attribute_01`", an attribute with sequence 2 gets ID "`attribute_02`", and so on. This simplifies your code migration.

Creating New Attributes

For new attributes created after moving to APEX 24.2, use whatever Static ID you wish. We recommend keeping the Static ID short, lowercase, and descriptive of the purpose. For example, "`css_classes`", "`page_item_name`", or "`plsql_code`".

The new attributes construct is also available for `t_plugin` in order to read application-scope attributes.

Public Dictionary Views

Public dictionary views are changed. Querying item plug-in attributes is now done by reading the attribute's JSON column.

```sql
select
i.attributes.my_static_id
  from apex_application_page_items
i
 where ...
```

This also applies when reading application-scope and Interactive Grid column attributes, Faceted Search filters, and Smart Filters filters.

### 2.16 Export App Enhancements

When you export a translated application, APEX checks the application to ensure that the translations are in sync. If the translations are out of sync, a warning message displays on the Application Export Page.

Select View Application Translations to check the translations for the application, and update them as needed. For more on translating applications, see Translating Messages in Oracle APEX App Builder
User’s Guide.

### 2.17 Default RTL Direction Based on Language

The Document Direction attribute on the Application Globalization page and Translation Language Mappings page now defaults to `Language Default` instead of `left-to-right`. When an application set to `Language Default` runs, the direction is now derived from the language.

There is no change of functionality for existing applications.

### 2.18 Builder Extension Auto-Subscribe

Instance Administrators can now configure the **Allow Hosting Extensions** option to allow **Automatic Subscription**. When a workspace is set up for automatic subscription, APEX automatically publishes all extensions and extension menu entries to all other workspaces in the instance. Individual workspaces no longer have to subscribe and grant read access to extensions manually.

### 2.19 Text Messages Enhancements

Comments and Metadata

The Create/Edit Text Message dialog now includes **Comments** and **Metadata**.

Use the Comments text area field to capture developer comments associated with a specific text message.

Use the Metadata region to capture any additional data for the text message, including:

* structured attributes that provide JSON name/value pairs to identify details about the text message related to an external central string repository
* unstructured data that provides further context to the text message to assist with translation

The Metadata region is a Collapsible region that only displays if metadata has been loaded via the PL/SQL API. Otherwise, the region is not visible.

Display Text Message Values

In Page Designer, the new Text Messages Picker (Page Designer, Utilities, Show) controls the visibility of the Text Messages dialog buttons (globe icon). If enabled, this button opens a Text Messages dialog that lists all available Text Messages in the current application.

When a text message is used in these properties, APEX displays a preview of the content below the input field.

The available text messages also display in the Suggestion box after typing `&{` in Code Editor.

This functionality requires the compatibility mode of the application to be set to 24.2 or higher.

### 2.20 New Substitution String

The new substitution string `MAIN_APP_ID` identifies the main application ID if the current application is a working copy. Otherwise, it shows the current application ID.

| Reference Type | Syntax |
| --- | --- |
| Bind variable | `:MAIN_APP_ID` |
| PL/SQL | `NV('MAIN_APP_ID')` |
| Substitution string | `&MAIN_APP_ID.` |

### 2.21 Application User Experience Data (OpenTelemetry)

You can now use **OpenTelemetry** for collecting user experience data, including page load times and user interactions. Configure OpenTelemetry through Workspace Utilities, and then add it to specific applications to make it easier to monitor and analyze how users engage with your app.

OpenTelemetry requires the latest version of Universal Theme.

### 2.22 Generative AI Configuration Screen Enhancements

The **Generative AI Service Details** page in Workspace Utilities now includes a Test Connection button that validates the information used for creating a Generative AI service connection. Test Connection performs a pre-validation of configuration parameters such as API keys, URLs, and model identifiers depending on the provider used. By running this check, you can quickly identify and edit any missing or incorrect fields before proceeding.

For more information, see Creating a Generative AI Service Object in Oracle APEX App Builder
User’s Guide.

### 2.23 Improved Content-Security-Policy Support

The APEX runtime engine adheres more strictly to Content-Security-Policy (CSP) standards by minimizing the use of unsafe-inline directives:

* Inline JavaScript: Inline event handlers are moved to external JavaScript files wherever possible. When not feasible, they are securely emitted using a unique identifier called a **nonce**.
* Inline CSS: Inline styles are now either moved to external CSS files, replaced with placeholder strings, or securely emitted using a nonce.
* Style Tags: `<style>` tags are securely emitted using a nonce.
* Script Tags: `<script>` tags are securely emitted using a nonce.

These changes enhance security by reducing risks associated with inline code.

For more information on configuring CSP in APEX, see Configuring Content Security Policy (CSP) in Oracle APEX
Administration Guide.

### 2.24 Improved Popup LOV Functionality

The appearance and behavior of Popup LOVs is now similar to searchable LOV items such as Select One, Select Many, and Combobox. This creates a unified and intuitive user experience when searching.

Popup LOVs have a new attribute **Match Type**, which you can set to Contains (default) or Starts With. There is also a control for **Case-Sensitive Search**.

### 2.25 Accessibility Improvements

Workflow Designer Keyboard Improvement

When navigating through Workflow Designer using keyboard shortcuts, the diagram viewport now follows the keyboard focus. It is no longer possible for the focused node to be outside the diagram viewport.

### 2.26 Theme Metadata Decoupled from Application Metadata

Starting with Universal Theme 24.2, theme metadata (templates, theme styles, template components, etc.) is now stored in a central workspace, decoupled from applications. This improves performance with faster application export/import, smaller file sizes, and optimized storage in version control systems.

Related updates include:

* The Refresh Theme button is now on the Application Home Page for better visibility.
* Outdated APEX Builder pages related to theme management have been updated or removed, simplifying the interface.
* Active theme style selection has moved from the theme style level to the theme level.

Important:

If your app uses translations, republish them after refreshing your theme, or translations will not work.

### 2.27 Select Many Improvements

If you set **Display Values As** to Comma-separated List. there is now a counter icon on the item that displays the current number of selected values. Clicking on the counter opens the dropdown, displaying only the selected values.

### 2.28 Universal Theme Enhancements

Font APEX 2.4

Font APEX now includes 244 country flag icons to easily display flags within your APEX application. Display the new icons with `.fa-flag-##`, where `##` is the country code.

See Accessing Font APEX in the Oracle APEX App Builder
User’s Guide.

Password Item Enhancements

**Password** type page items now include a Show Password button. Users can select Show Password to reveal the entered password, and select Hide Password to conceal the password again.

This button is enabled by default for all application using Universal Theme 24.2 and later. To disable this button, edit the template options for the **Password** item, and select Hide Password Visibility.

Other Changes

Other changes for Universal Theme 24.2 include:

* new utility classes for Typography, Shadows, Flex Order, and Padding/Margin
* support for grouping in Content Row (title and icon)
* display for multiple Avatars in the Avatar Template Component
* better support for mobile browsers with dynamic toolbars
* miscellaneous updates to Redwood Light, including adjustment of page padding to be consistent with Vita

### 2.29 PL/SQL API Updates

APEX_APPLICATION_ADMIN

The new procedure `APEX_APPLICATION_ADMIN.SET_REMOTE_SERVER` changes the base URL of a Remote Server object after deployment of an application.

APEX_CREDENTIAL

The `APEX_CREDENTIAL` API is extended with a new procedure: `SET_SCOPE`. This procedure programmatically changes the "scope" attribute of a web credential.

APEX_LANG

The existing procedure `CREATE_MESSAGE` is enhanced with two new parameters:

* `p_comment`, for developer comments or notes only visible in the App Builder
* `p_metadata`, for additional data stored alongside the message

A new procedure, `UPDATE_MESSAGE`, can update all attributes of a text message.

APEX_PAGE

The `GET_URL` procedure has a new boolean parameter: `p_absolute_url`. When set to `FALSE`, the function determines whether an absolute URL is needed. When set to `TRUE`, the function always generates an absolute URL.

APEX_REGION

Many APEX API functions take `p_region_id` as an input. The new function `GET_ID` retrieves the region id from the APEX dictionary views.

APEX_SHARED_COMPONENT

The new `APEX_SHARED_COMPONENT` package contains two APIs for working with shared components: `REFRESH` and `PUBLISH`. This package is only available in full APEX installations, and does not apply to theme refresh and publish.

### 2.30 JavaScript API Updates

New and Updated APIs

This release contains new and updated APIs:

* New `apex.message` namespace functions:
  + `ariaAlertMessage`
  + `ariaMessage`
* New `actions` interface `action` property `convertBindingArguments`.
* New syntax for text messages added to `apex.util.applyTemplate`. This syntax requires compatibility mode 24.2.
* Interface `region refresh` method documents `pKeepPagination` parameter used by some regions.
* Widget `interactiveGrid` now documents the `text` option including new property `noParentSelected`.
* Changes to `facetsRegion` interface for new Faceted Search Add Filter feature:
  + Removed control property `displayed` and replaced it with new property `displayAs`.
  + Methods `addChart`, `hideFacet`, and `showFacet` only work when `displayAs` is "INLINE".
* Changes related to reports based on `grid` or `tableModelView` widgets not clearing old content while fetching new content:
  + New `model` option `delayClearData` added to `apex.model.create`, which can also be set by `model` method `setOption`.
  + The `check` and `clearData` methods describe the new behavior related to `delayClearData`.
  + Interface `model refresh` notification has new `changes` property `clearDataPending`.
  + Interface `model` method `forEachInPage pCallback` function can receive a false value for the `pError` parameter.
* Changes related to nested markup for control breaks
  + New `model` interface methods `getControlBreakId` and `hasControlBreaks`.
  + Interface `model` method `insertNewRecord` now initializes control break fields.
  + New `model FieldMeta` property `controlBreakIndex`.
  + Interface `model` method `setSelectionState` has a new value for `pAction` parameter.
  + Widget `tableModelView` adds options `controlBreakAfterTemplate`, `controlBreakBeforeTemplate`, and `controlBreakSelector`. Option `controlBreakTemplate` has new substitutions and now requires setting the `controlBreakSelector` option.
  + Widget `tableModelView` methods `getCurrentItem`, `getCurrentItemValue`, `setCurrentItem` apply when focus is on a group heading.

Updated Descriptions, Examples, or Typos Fixed

This release includes various improvements to descriptions and examples.

### 2.31 JavaScript Library Upgrades

* @opentelemetry/api 1.9.0
* @opentelemetry/core 1.26.0
* @opentelemetry/instrumentation 0.53.0
* @opentelemetry/instrumentation-document-load 0.39.0
* @opentelemetry/instrumentation-fetch 0.53.0
* @opentelemetry/instrumentation-xml-http-request 0.53.0
* @opentelemetry/sdk-trace-base 1.26.0
* @opentelemetry/sdk-trace-web 1.26.0
* Cohere API Spec 7.9.5
* cropperjs 1.6.2
* DomPurify 3.1.6
* FullCalendar 6.1.15
* JavaScript Extension Toolkit (JET) 17.0.2
* jquery-migrate 3.5.2
* mapbox-gl-rtl-text 0.3.0
* MapLibre GL 4.6.0
* Marked 14.1.0
* Monaco Editor 0.51.0
* OpenAI OpenAPI Spec 2.0.0
* Oracle Rich Text Library (ORTL) 2.0.1
* Pako 2.1.0
* Terser 5.31.3
* Turndown 7.2.0

---

<!-- fonte: htmrn/changed-behavior.html -->
## 3 Changed Behavior

Some existing behaviour changes in this release.

* Theme Style Selection
* Unified Task List and Workflow Console Compatibility Mode
* Improved Search Input Field on Search Pages
* Improved Map Labels
* Change to Interactive Grid Report Display During Refresh
* Page Import Changes
* Changes to Modal Dialog Page URLs
* Refresh Dynamic Action Changes
* Shared Component Navigation Changes
* Changes to Public Dictionary Views
* Control Break Customization (tableModelView)
* Changes to Faceted Search Arbitrary Filters
* Show AI Assistant Dynamic Action
* Edit List Simplified
* Text Message Substitution Strings
* Column Toggle Report, List View, and Reflow Report now Legacy
* App Builder UI Changes
* Compatibility Mode
* Enabling Network Services in Oracle Database
  Database administrators must enable network services in Oracle Database to send outbound mail, invoke web services, or use template-based PDF report printing with external print servers in Oracle APEX.

### 3.1 Theme Style Selection

In APEX Builder under Shared Components, User Interface Attributes, the option **Enable End Users to Choose Theme Style** lets users select from the available theme styles by using Customize in the runtime app footer.

Starting with APEX 24.2, if your app subscribes to Universal Theme 24.2, you can no longer use the Public flag to control the visibility of Oracle-provided theme styles like Vita and Redwood Light. This is because Oracle-provided theme styles now belong to a centralized Universal Theme repository, not the current application. This change does not affect custom theme styles.

### 3.2 Unified Task List and Workflow Console Compatibility Mode

The **Unified Task List** and **Workflow Console** pages now use enhanced substitution strings. In order for APEX to create these pages, compatibility mode must be set to 24.2 or higher.

### 3.3 Improved Search Input Field on Search Pages

The default behavior for new search pages created by the Create Page Wizard is improved.

The **search field** now has:

* a larger input field (`xlarge` instead of `large`)
* item `css class` set to `mxw80 t-Form-fieldContainer--noPadding`
* text placeholder set to `Search...`

The **search region** now has:

* a default **no query entered** message (`Please enter your search term.`)
* a default **no results found** message (`No results for your search term.`)

### 3.4 Improved Map Labels

Right-to-left (RTL) language labels now display correctly on Map Regions.

### 3.5 Change to Interactive Grid Report Display During Refresh

Previously, Interactive Grid would clear the report during any kind of refresh, including when the sort or filter changed. Now, Interactive Grid displays the previous report until the new results arrive. The progress indicator behaves the same, but data loading now appears smoother.

To restore the previous behavior, add the below code to the region Initialization JavaScript Function attribute:

```sql
function( config ) {
    config.defaultModelOptions = {
        delayClearData: false
    };
    return config;
}
```

### 3.6 Page Import Changes

You can now import a page into a different application or workspace without needing to use the command line. This allows more efficient page-level imports through the App Builder interface, streamlining the import process.

### 3.7 Changes to Modal Dialog Page URLs

APEX no longer generates `javascript:` URLs for modal dialog pages. This improves the support for Content-Security-Policy settings. This change could impact your applications when you:

* manipulate the URL in the browser using JavaScript
* rely on the URL being a JavaScript function in your code

An example of custom code that no longer works is a button with an `onclick` attribute to open a modal dialog page. You should search for `onclick=` in your code:

```sql
<button onclick="dialog_url">Click here</button>
```

A workaround is to use the `data-action` attribute of the button:

```sql
<button data-action="dialog_url">Click here</button>
```

There is a new way to open modal dialog pages using JavaScript in the browser. You can use `apex.navigation.dialog`. The URL can be the return value of `APEX_PAGE.GET_URL`, even for dialog pages. For example:

```sql
apex.navigation.dialog(
     apex.items.P1_DIALOG_URL.value,
     {
        height:'480',
        width:'800',
     } );
```

The `p_triggering_element` parameter of the `apex_util.prepare_url` and `apex_page.get_url` APIs can no longer be a JavaScript expression. The value now must be a string selector.

For example, use `#STATIC_ID` instead of `$('#STATIC_ID')`.

```sql
select apex_page.get_url(
           p_application        => 100,
           p_page               => 2, -- a modal dialog page
           p_triggering_element => '#STATIC_ID' ) as url
  from dual;
```

### 3.8 Refresh Dynamic Action Changes

The Refresh dynamic action now features a Maintain Pagination switch. If the switch is `On`, pagination and scroll position for reports is maintained on refresh.

This switch is currently only supported for Interactive Reports.

### 3.9 Shared Component Navigation Changes

Some Shared Components are now located under different headings:

* Map Backgrounds moves from **Other Components** to **User Interface**
* Data Load Definitions moves from **Data Sources** to **Other Components**
* REST Enabled SQL Databases moves from **Data Sources** to Workspace Objects
* REST Synchronizations moves from **Data Sources** to Tasks

Generative AI features move to the **Generative AI** section:

* AI Attributes
* AI Configurations
* AI Services

### 3.10 Changes to Public Dictionary Views

In the following public dictionary views, the columns attribute_01...25 now return null:

* `apex_application_page_items`
* `apex_appl_page_ig_columns`
* `apex_appl_page_filters`
* `apex_appl_plugin_settings`

Use the JSON attributes column instead.

### 3.11 Control Break Customization (`tableModelView`)

Any custom code that used the `tableModelView` widget `controlBreakTemplate` option to implement control breaks now requires changes:

* add the new `controlBreakSelector` option
* add the `model` FieldMeta property `controlBreakIndex` to all break columns
* use the new #APEX$GROUP_IDENTIFICATION# placeholder

See the JavaScript API documentation for full details.

### 3.12 Changes to Faceted Search Arbitrary Filters

The Display Toggling property is no longer part of faceted search. Instead, use the new Display property, and select whether facets are displayed Inline, or in an Add Filter Dialog. If you select Add Filter Dialog, the facets display in a modal dialog page.

You can right-click Facets in Page Designer to **Synchronize Facets** and quickly add new facets to existing regions.

### 3.13 Show AI Assistant Dynamic Action

The "Show AI Assistant" dynamic action's JavaScript Code attribute, used for custom processing of the assistant's responses, now binds the value of the response differently. Previously, the response was available simply as "`this`". Now, the response should be accessed as "`this.data.response`".

### 3.14 Edit List Simplified

In Shared Components, Lists, Edit List, the List Entries now display as an Interactive Report. To edit a list entry, you must select the List Entry Name to go to the Edit List Entry page.

To use an Interactive Grid to edit list entries, select Grid Edit from the Tasks list when editing a list.

### 3.15 Text Message Substitution Strings

To reference text messages, you can now wrap the message name in curly brackets. For example, to reference text message `TEXT.MSG`, you can use `&{TEXT.MSG}`. Text message substitution also supports parameters. Before the closing bracket, add `name=value` pairs, separated by white space.

This syntax is only available if the application's Compatibility Mode is set to 24.2 or higher. For more information, see Substitutions in Text Messages (24.2 or later) in Oracle APEX App Builder
User’s Guide.

### 3.16 Column Toggle Report, List View, and Reflow Report now Legacy

The Column Toggle Report, List View, and Reflow Report are now marked Legacy.

### 3.17 App Builder UI Changes

Changes to the application builder user interface for this release include:

* The dynamic action **Open AI Assistant** is renamed to **Show AI Assistant**.
* Modal dialog pages can now be declaratively set as Resizable.
* Application ID, Page ID, and Page Name are now displayed in Page Designer.
* The Page Number field now supports up to eight characters.
* For Popup LOVs, the Search as You Type attribute is now named Fetch on Search. The Minimum Characters field is now moved to the **Search** subarea.

### 3.18 Compatibility Mode

The application attribute **Compatibility Mode** controls the compatibility mode of the APEX runtime engine. Certain runtime behaviors change from release to release. You can use the Compatibility Mode attribute to obtain specific application behavior. This section lists Compatibility Mode changes by release. Note that all mode changes are inclusive in that all changes in older releases are included in newer releases.

Compatibility Mode Changes in Mode 4.1

In Oracle Application Express release 4.1, Automatic DML forms raised an error when rendering the page if the column name of the source of an item was invalid. Prior to Oracle Application Express release 4.1, an invalid column name of the source of an item would not raise an error when rendering the page but it would also not set session state of the item.

Also, in Oracle Application Express release 4.1, there are two new application Security Attributes to control Browser Security: **Cache** and **Embed in Frames**. Enabling the Cache attribute enables the browser to save the contents of your application's pages in its cache, both in memory and on disk. The Embed in Frames attribute controls if the browser displays your application's pages within a frame. Applications running in a Pre-4.1 Compatibility Mode function as if the Cache is enabled and as if Embed in Frames is set to allowed. Applications running in Compatibility Mode 4.1 or later respect the specific Browser Security attributes.

Also, in Oracle Application Express release 4.1, because of bug 12990445, the following changes were implemented for Automatic Row Processing (DML) process types. The code which performs the INSERT was changed to determine if the columns should be included in the INSERT statement. Note that these are the same checks which occur before an UPDATE. These new checks include:

* Is the source type a DB Column?
* Is the page item contained in the POST request? For example, if the page item is conditional it will not be contained in the POST request if the condition evaluates to FALSE during page rendering.
* Is the page item not of type Display Only where Save State is set to No?

To enable these behaviors, set the Compatibility Mode to 4.1 or later. For behavior that matches earlier releases, set the Compatibility Mode to Pre-4.1.

Compatibility Mode Changes in Mode 4.2

In Oracle Application Express release 4.2 due to changes for the new grid layout, when a page is rendered, all regions in a certain display point are evaluated before rendering that display point, to find out if they should be displayed or not (so that the grid layout knows how many columns to render). The regions where the evaluation returned true will be executed and displayed. However, this will not work if a PL/SQL based region sets session state which is then used in a subsequent region condition to determine if the region should be displayed. In that scenario, the condition has already been checked before the display point is rendered. Use computations or PL/SQL processes to set session state before any region is displayed. In previous versions, the condition was evaluated right before each region was displayed.

In Oracle Application Express release 4.2, computations and processes with a processing point Before Region(s) do now fire before any region gets rendered. Computations and processes with a processing point After Region(s) fire after all regions have been rendered. In previous versions, the computations and processes fired just before and after the region display point Page Template Body (1-3).

Oracle Application Express Patch Set 4.2.2 added two new Compatibility Mode changes for Compatibility Mode 4.2:

* Text areas were changed to always use the Maximum Width attribute to restrict text input.
* Enhanced security for report column links, where the link contains both JavaScript and references to other report column substitutions, for example:

  ```sql
  javascript:alert( 'Delete #NAME#' );
  ```

  In the previous example, `NAME` is a column name in the report.

Prior to Oracle Application Express release 4.2.1, to protect against possible cross-site scripting vulnerabilities, you would have had to explicitly escape any column values in the report source, so that they could safely be used in JavaScript links. When running in Compatibility Mode 4.2, Oracle Application Express automatically JavaScript escapes column name substitutions referenced in JavaScript links if the column is defined to escape special characters.

To fix this, Oracle recommends that you remove the manual JavaScript escaping from your report source and use of the native escaping.

Compatibility Mode Changes in Mode 5.0

In Oracle Application Express release 5.0, referencing a Static Application File with `#WORKSPACE_IMAGES#` no longer returns the application file. Instead, use `#APP_IMAGES#`.

The API calls to `wwv_flow_custom_auth_std.logout`, `wwv_flow_custom_auth_std.logout_then_go_to_page`, `wwv_flow_custom_auth_std.logout_then_go_to_url`, and `apex_custom_auth.logout` are desupported and will raise a runtime error instead of logging out from the Oracle Application Express session. Instead, use the `apex_authentication.logout` entry point.

Prior to release 5.0, developers using data upload did not have the option to choose a date format. Instead, a parser checked for the best format to match the user's entry or an end user could enter their own format. Oracle Application Express release 5.0 includes a new item that enables the user to choose an application date format or user entered format. Because applications created before release 5.0 do not have an item, a Compatibility Mode of 5.0 checks if the user has entered some data. If no data has been entered, it picks the application date format.

When a session timeout occurs and no timeout URL is specified, Oracle Application Express raises an error instead of redirecting to the application's home page. If the session setup for an Ajax requests fails, Oracle Application Express also raises an error. For Ajax requests that expect JSON, the response is a JSON string with members that describe the error. For other requests, the error appears on an error page.

Page items based on a database column where the attribute Source Used is set to Only when current value in session state is null will raise an error when the page item gets rendered. Using this setting for a database column is very dangerous and can result in accidentally overwriting data when viewing and saving multiple records. Always set the Source Used attribute to Always, replacing any existing value in session state.

Compatibility Mode Changes in Mode 5.1 / 18.1 / 18.2

In Oracle Application Express 18.1, buttons where the Execute Validations attribute is set to Yes also perform some client-side validations (such as item required checks) and will not submit the page until all issues are fixed. In previous versions this flag was just used to determine if server-side validations should be executed.

Tip:

Please pay attention when changing the Compatibility Mode to 5.1/18.1/18.2. Buttons, such as Cancel or Previous, where the Execute Validation flag has incorrectly been set to Yes and which use an After Submit branch, never execute validations when the user clicks the button. You can address this issue by using the new client-side validations, or by setting Execute Validations to No.

In release 5.1, any Ajax-based Dynamic Actions where the "Wait for Result" attribute is set to `Yes` perform an asynchronous Ajax call. Prior to 5.1, such calls would be made synchronously.

Compatibility Mode Changes in Mode 19.1

In Oracle Application Express 19.1, the Rich Text editor now enforces validation of the `Max Length` item attribute. When the length of the HTML markup exceeds the `Max Length` value, the system produces an error message.

Compatibility Mode Changes in Mode 19.2 / 20.1 / 20.2 / 21.1

In Oracle Application Express 19.2, Classic Reports render empty column values as an empty cell instead of using a "non-breaking white-space" (`&nbsp;`).

Compatibility Mode Changes in Mode 21.2 to 24.1

Prior to Oracle Application Express 21.2, all processes of the current processing point have been executed regardless of the added errors.

In Oracle Application Express 21.2, calling `APEX_ERROR.ADD_ERROR` in a process stops further processes from executing and immediately displays the inline errors.

Compatibility Mode Changes in Mode 24.2

Starting with release 24.2, APEX supports an extended substitution syntax for text messages: `&{TEXT.MESSAGE}`.

### 3.19 Enabling Network Services in Oracle Database

Database administrators must enable network services in Oracle
Database to send outbound mail, invoke web services, or use template-based PDF report printing with external print servers in Oracle APEX.

To learn more, see Enabling Network Services in Oracle Database
in Oracle APEX Installation
Guide.

Note:

Enabling network services does not apply to APEX instances running on Oracle
Autonomous Database. APEX can communicate with external endpoints over the internet without additional
configuration.

* When and Why Network Services Must be Enabled
  Enabling network services enables support for sending outbound mail in Oracle APEX, using REST Services, REST Enabled SQL, or other web services, and using a remote server for report printing.
* Granting Connect Privileges
* Troubleshooting an Invalid ACL Error
  Learn how to identify any invalid ACL error by running the query.

#### 3.19.1 When and Why Network Services Must be Enabled

Enabling network services enables support for sending outbound mail in Oracle APEX, using REST Services, REST Enabled SQL, or other web services, and using a remote server for report printing.

By default, the ability to interact with network services is disabled in Oracle Database. Therefore, you must use the `DBMS_NETWORK_ACL_ADMIN` package to grant network connect privileges to the database user that owns the APEX schema (`APEX_240200`). Failing to grant these privileges results in issues with:

* Sending outbound mail in Oracle APEX.

  Users can call methods from the `APEX_MAIL` package, but issues arise when sending outbound email.
* Consuming REST services and other web services from APEX.
* Making outbound LDAP calls from APEX.
* Using a remote print server for report printing.

The granted network connect privileges apply to the entire APEX instance and enable all applications in all workspaces to perform outbound network calls. You do not need to grant network connect privileges to individual workspace schemas unless applications also use native database PL/SQL API such as `UTL_HTTP` and `UTL_SMTP`.

Note:

When upgrading APEX, the upgrade automatically configures Network Services based on the configuration of the previous APEX version.

Tip:

To run the examples described in this section, the compatible initialization parameter of the database must be set to at least `11.1.0.0.0`. By default, the parameter is set properly, but a database upgraded from a version prior to 11g may require an update. For information about changing database initialization parameters, see Specifying the Database Compatibility Level in Oracle Multitenant
Administrator's Guide.

See Also:

About Report Printing in Oracle APEX App Builder
User’s Guide.

#### 3.19.2 Granting Connect Privileges

The following example demonstrates how to grant connect privileges to any host for the the database user that owns the APEX schema (`APEX_240200`). This example assumes you connected to the database where Oracle APEX is installed as `SYS` specifying the `SYSDBA` role.

```sql
BEGIN
    DBMS_NETWORK_ACL_ADMIN.APPEND_HOST_ACE(
        host => '*',
        ace => xs$ace_type(privilege_list => xs$name_list('connect'),
                           principal_name => APEX_APPLICATION.g_flow_schema_owner,
                           principal_type => xs_acl.ptype_db));
END;
/
```

The following example demonstrates how to provide less privileged access to local network resources. This example enables access only to servers running on the same database host (`localhost`), such as email and report printing servers.

```sql
BEGIN
    DBMS_NETWORK_ACL_ADMIN.APPEND_HOST_ACE(
        host => 'localhost',
        ace => xs$ace_type(privilege_list => xs$name_list('connect'),
                           principal_name => APEX_APPLICATION.g_flow_schema_owner,
                           principal_type => xs_acl.ptype_db));
END;
/
```

#### 3.19.3 Troubleshooting an Invalid ACL Error

Learn how to identify any invalid ACL error by running the query.

If you receive an `ORA-44416: Invalid ACL` error after running the previous script, use the following query to identify the invalid ACL:

```sql
REM Show the dangling references to dropped users in the ACL that is assigned
REM to '*'.

SELECT ACL, PRINCIPAL
  FROM DBA_NETWORK_ACLS NACL, XDS_ACE ACE
 WHERE HOST = '*' AND LOWER_PORT IS NULL AND UPPER_PORT IS NULL AND
       NACL.ACLID = ACE.ACLID AND
       NOT EXISTS (SELECT NULL FROM ALL_USERS WHERE USERNAME = PRINCIPAL);
```

Next, run the following code to fix the ACL:

```sql
DECLARE
  ACL_ID   RAW(16);
  CNT      NUMBER;
BEGIN
  -- Look for the object ID of the ACL currently assigned to '*'
  SELECT ACLID INTO ACL_ID FROM DBA_NETWORK_ACLS
   WHERE HOST = '*' AND LOWER_PORT IS NULL AND UPPER_PORT IS NULL;

  -- If just some users referenced in the ACL are invalid, remove just those
  -- users in the ACL. Otherwise, drop the ACL completely.
  SELECT COUNT(PRINCIPAL) INTO CNT FROM XDS_ACE
   WHERE ACLID = ACL_ID AND
         EXISTS (SELECT NULL FROM ALL_USERS WHERE USERNAME = PRINCIPAL);

  IF (CNT > 0) THEN

    FOR R IN (SELECT PRINCIPAL FROM XDS_ACE
               WHERE ACLID = ACL_ID AND
                     NOT EXISTS (SELECT NULL FROM ALL_USERS
                                  WHERE USERNAME = PRINCIPAL)) LOOP
      UPDATE XDB.XDB$ACL
         SET OBJECT_VALUE =
               DELETEXML(OBJECT_VALUE,
                         '/ACL/ACE[PRINCIPAL="'||R.PRINCIPAL||'"]')
       WHERE OBJECT_ID = ACL_ID;
    END LOOP;

  ELSE
    DELETE FROM XDB.XDB$ACL WHERE OBJECT_ID = ACL_ID;
  END IF;

END;
/

REM commit the changes.

COMMIT;
```

Once the ACL has been fixed, you must run the first script in this section to apply the ACL to the `APEX_240200` user.

---

<!-- fonte: htmrn/deprecated-features.html -->
## 5 Deprecated Features

Deprecated features are features which Oracle plans to desupport or remove in a future release of Oracle APEX. If a feature is related to application metadata or an API, existing applications can still use the feature, but Oracle strongly recommends that developers start to modify their applications as described in this section. Use APEX Advisor to scan existing applications for deprecated attributes.

* Deprecated APIs

### 5.1 Deprecated APIs

APEX_LANG

`APEX_LANG.MESSAGE` is deprecated. Instead, use `APEX_LANG.GET_MESSAGE` to support named substitution parameters.

APEX_PLUGIN_UTIL

`APEX_PLUGIN_UTIL.EXECUTE_PLSQL_CODE` is now deprecated. Instead, use `APEX_EXEC.EXECUTE_PLSQL` Signature 1 or Signature 2.

APEX_UTIL

In `APEX_UTIL`, the following APIs are deprecated:

* `custom_calendar`
* `increment_calendar`

---

<!-- fonte: htmrn/desupported-features.html -->
## 7 Desupported Features

Desupported features are no longer available. If a desupported feature has to do with application metadata or APIs, then existing applications may not work as they did previously. Oracle recommends modifying the application to replace the feature.

* Desupported APIs
* Public Dictionary View Changes
* TinyMCE-based Rich Text Editor Desupported
* CSSO Desupported

### 7.1 Desupported APIs

As of APEX 24.2, the following APIs are desupported:

* `apex_javascript.add_3rd_party_library_file`
* `apex_css.add_3rd_party_library_file`

### 7.2 Public Dictionary View Changes

As of APEX 24.2, columns `attribute_01` through `attribute_25` now return null in the following views:

* `apex_application_page_items`
* `apex_appl_page_ig_columns`
* `apex_appl_plugin_settings`
* `apex_appl_page_filters`

You can query this attributes by reading the attribute's JSON column. See Unlimited Attributes for Item Plug-ins.

### 7.3 TinyMCE-based Rich Text Editor Desupported

In APEX 24.1, the Rich Text Editor page item based on the TinyMCE library was deprecated.

As of APEX 24.2, TinyMCE is desupported and the Rich Text Editor page item no longer supports the TinyMCE library. The underlying library is now Oracle Rich Text Library (ORTL). Any Rich Text Editor page items still using TinyMCE are auto-migrated to ORTL. Any custom Initialization JavaScript Function code is commented out.

### 7.4 CSSO Desupported

The CSSO 3rd party JavaScript library is removed from APEX, and replaced with a basic minification logic. This may impact existing CSS static files.

---

<!-- fonte: htmrn/open-bugs-known-issues.html -->
## 10 Open Bugs and Known Issues

This section describes bugs and known issues for Oracle APEX release 24.2.

Tip:

This section is current as of the writing of this document. To view the most current listing of changed behavior, go to the Known Issues page:

https://www.oracle.com/tools/downloads/apex-downloads/apex-242-known-issues/

Alternatively, you can view the Accessibility Conformance Report (ACR). The ACR includes details of all known issues with APEX. A single release of APEX uses multiple component ACRs for specific areas of the product (for example, "Development Environment", "Components", "Documentation", etc.) Please go to Accessibility ACRs | Oracle's Accessibility Program to find the ACRs for Oracle APEX.

* Known Issue with Document Generator
* Known Issue with Theme Decoupling
* Known Issues with Using BOSS REST Services
* Known Issue with ORDS 24.1 and APEX SQL Developer Web
* Known Issue for Sublists
* Known Issues for Working Copy Feature
* Known Issues for Workflow Component
* Known Issue with Confirm or Alert Dynamic Action Messages When Upgrading
* Known Issue using 'Source Display' region type plug-in in previously installed Sample Apps
* Known Issues for jQuery Upgrade
* Interactive Grid support for REST Enabled SQL
* Group By Component Type mode prevents Default View
* Known Issues for Data Generator

### 10.1 Known Issue with Document Generator

When you create a `DBMS_CLOUD` OCI API Key Credential in APEX 24.1 and use it as a credential for Document Generator, the credential is missing after upgrading to APEX 24.2.

The fix for this issue is added in APEX 24.2.4. Any credential created in APEX 24.2.4 or later will not be missing after an upgrade.

### 10.2 Known Issue with Theme Decoupling

There is a known issue with theme decoupling in the following scenario:

1. A Master theme app and a child theme app are defined in the same workspace.
2. The Master theme app is subscribed to the UT in the central application, and the child theme app is subscribed to the Master theme app.
3. The Master theme app hosts some locally-defined templates that don't exist in the central application.

In this scenario, if you refresh the child app theme, it does not copy the Master theme's locally-defined templates over to the child app. As a workaround, you can copy the locally-defined templates manually.

### 10.3 Known Issues with Using BOSS REST Services

Total Results Only Works with Search Views

BOSS support for total results currently only works on search views.

Error Defining REST Data Source Against OAuth-Protected BOSS Endpoint in RDBMS 19c

If your APEX is running in an Oracle 19c database, then when initially defining a REST Data Source against an OAuth-secured BOSS endpoint, you may encounter an `HTTP 401 Not Authorized` error when discovering the service. The error text returned could indicate `Anonymous Access is not allowed for OpenApi Service`.

The solution is to use the fully-qualified BOSS endpoint URL including both the optional language path segment (for example, `$en`) and an explicit deployment id after the version path segment. For example, instead of referencing `.../v1/exampleobject` you would use `.../v1:99/$en/exampleobject` during discovery. Once the REST Data Source is created, you can edit its service URL to remove the language path segment and the explicit deployment id.

### 10.4 Known Issue with ORDS 24.1 and APEX SQL Developer Web

When on an upgraded APEX 24.1 instance using ORDS version 24.1.0, if you click the link from APEX App Builder to SQL Developer Web, an error message ("Method Not Allowed") appears.

This bug is fixed in ORDS version 24.1.2.

### 10.5 Known Issue for Sublists

Currently, sublist entries are not included in list search results when the list search configuration is defined on the list referencing the sublist. This will be fixed in a future release.

### 10.6 Known Issues for Working Copy Feature

The known issues for the working copy feature are:

* **Server Error** message - If you are running APEX on Oracle
  Database release 19c and using the new working copy feature, when you choose the actions Merge into Main or Refresh from Main or Compare Changes, you may get a "Server Error" message that is caused by an underlying ORA-00600 error message. For example:

  ```sql
  ORA-00600: internal error code, arguments: [qjsnplsDecDomRefCnt:noValP], [], [], [], [], [], [], [], [], [], [], []
  ```

  The fix for this error is to upgrade to 19.16 or higher.
* **ORA-00001** error during merge - The Working Copy feature raises an ORA-00001 unique constraint error when attempting to merge changes for component names that are not unique. It is important to coordinate the naming of shared components across working copies and the main application to avoid this error occurring.

### 10.7 Known Issues for Workflow Component

The known issues for the Workflow Component are:

* The workflow title can only use workflow parameters as substitution strings, but not any additional data source columns
* When using Workflow Designer in a Safari browser, arrows become straight lines in the Workflow Diagram Builder and the type text disappears under the Additional Data Property for workflow version.
* Terminating a Workflow does not auto-cancel the human task(s) created while executing the workflow.
* When deleting a workflow using the `Delete` key on the keyboard, there is no warning message. Deleting a workflow by right-clicking the workflow and selecting Delete provides a warning message and a prompt for user confirmation.

### 10.8 Known Issue with Confirm or Alert Dynamic Action Messages When Upgrading

Issue

When upgrading from APEX 21.2 or earlier, the text in existing Confirm or Alert dynamic action messages may be truncated if it is too long, leading to data loss. This is due to APEX HTML-escaping messages, which may increase their size past the 4000-byte limit.

Resolution

Prior to upgrading, run a query to check whether any messages are affected:

```sql
select *
    from apex_application_page_da_acts
where action_name in ('Alert', 'Confirm')
    and ( lengthb( attribute_01 )
        + ( 4 * nvl( regexp_count( attribute_01, '&|"|<|>' ), 0 ) )
        ) > 4000;
```

If the query does not return any rows, proceed with the upgrade.

If the query does return rows, convert the affected rows into application text messages and reference them with substitution syntax before proceeding with the upgrade.

### 10.9 Known Issue using 'Source Display' region type plug-in in previously installed Sample Apps

Issue

The Source Display region type plug-in that is used in a Sample App installed in a previous release of APEX no longer works. This issue is due to the removal of views associated with AnyChart charts and AnyMap map charts.

Resolution

1. Open the application to edit it.
2. Navigate to Shared Components, under Other Components select Plug-ins, and Source Display.
3. Update the PL/SQL Code to remove the following lines of code (lines 35 - 48):

   ```sql
   union all
   select reg.source_type, fs.series_seq, fs.series_name, fs.series_query source
   from apex_application_page_regions reg,
       apex_application_page_flash5_s fs
   where reg.application_id = :APP_ID
       and reg.page_id = :APP_PAGE_ID
       and reg.static_id = d_region_static_id
       and fs.application_id = reg.application_id
       and fs.page_id = reg.page_id
       and fs.region_id = reg.region_id
       and reg.source_type in (
           'Flash Chart',
           'Map'
       )
   ```
4. Click Apply Changes.

### 10.10 Known Issues for jQuery Upgrade

jQuery 3.x breaks compatibility with earlier 2.x versions. For applications that still rely on removed 2.x functionality, you can use the jQuery Migrate plug-in (to include this plug-in, set the Desktop User Interface Details attribute **Include jQuery Migrate** to **Yes**).

If your application relies on removed 1.x jQuery APIs, that functionality no longer works as of Application Express release 18.1. You must update the JavaScript to only use jQuery 3.5 or later APIs. See the jQuery migration guides to learn more:

* To migrate from 1.x to 2.x see http://jquery.com/upgrade-guide/1.9/
* To migrate from 2.x to 3.5.x see https://jquery.com/upgrade-guide/3.5/

### 10.11 Interactive Grid support for REST Enabled SQL

Issue

Oracle REST Data Services (ORDS) REST Enabled SQL has a limit of 1000 bind variables in a REST Enabled SQL request. As a result, when Interactive Grid DML sends more than 1000 column values, the following error displays: "Internal ORDS OUT Bind limits exceeded."

Solution

Reduce the amount of DML rows.

### 10.12 Group By Component Type mode prevents Default View

Issue

Due to the removal of "Sort by Processing Order" and "Group by Component Type" from Page Designer, developers may be stuck in "Group by Component Type" mode without a way to switch back to the default view ("Sort by Processing Order").

Resolution

1. In Page Designer, open Developer Console in the browser, and run the following command:

   ```sql
   pageDesigner.saveBoolPref( "GROUP_BY_COMPONENT_TYPE", true );
   ```
2. Refresh the page.

### 10.13 Known Issues for Data Generator

There are known issues with the API for the data generator:

* API does not accept Percent Blank value of 100.
* Some built-ins that return a number data type ignore values set for minimum value, maximum value, and value precision.
* Preview ignores columns when all their values are null.
* When generating data and using row scaling other than 1x, sometimes an extra row is added.

These issues will be fixed in a future release.

