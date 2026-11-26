<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_PAGE (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_PAGE

The `APEX_PAGE` package is the public API for handling pages.

---

## Global Constants

The APEX_PAGE package uses the following constants.

```sql
c_ui_type_desktop   constant varchar2(10) := 'DESKTOP'; -- Deprecated
```

---

## GET_PAGE_MODE Function

This function returns the page mode for a given page.

Syntax

```sql
FUNCTION GET_PAGE_MODE (
    p_application_id IN NUMBER,
    p_page_id        IN NUMBER )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | `ID` of the application. |
| `p_page_id` | `ID` of the page. |

---

## GET_UI_TYPE Function (Deprecated)

Note:

This API is deprecated and will be removed in a future release.

This function returns the user interface (UI) type for which the current page has been designed.

Syntax

```sql
FUNCTION GET_UI_TYPE
RETURN VARCHAR2;
```

---

## GET_URL Function

Returns an APEX `f?p= URL`. It is sometimes clearer to read a function call than a concatenated URL. See the example below for a comparison.

Note:

The URL excludes a checksum if the specific application is located in a different workspace.

Syntax

```sql
APEX_PAGE.GET_URL (
    p_application        IN VARCHAR2 DEFAULT NULL,
    p_page               IN VARCHAR2 DEFAULT NULL,
    p_session            IN NUMBER   DEFAULT apex_application.g_instance,
    p_request            IN VARCHAR2 DEFAULT NULL,
    p_debug              IN VARCHAR2 DEFAULT NULL,
    p_clear_cache        IN VARCHAR2 DEFAULT NULL,
    p_items              IN VARCHAR2 DEFAULT NULL,
    p_values             IN VARCHAR2 DEFAULT NULL,
    p_printer_friendly   IN VARCHAR2 DEFAULT NULL,
    p_trace              IN VARCHAR2 DEFAULT NULL,
    p_x01                IN VARCHAR2 DEFAULT NULL,
    p_hash               IN VARCHAR2 DEFAULT NULL,
    p_triggering_element IN VARCHAR2 DEFAULT 'this',
    p_plain_url          IN BOOLEAN  DEFAULT FALSE,
    p_absolute_url       IN BOOLEAN  DEFAULT FALSE )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application` | The application ID or alias. Defaults to the current application. |
| `p_page` | Page ID or alias. Defaults to the current page. |
| `p_session` | Session ID. Defaults to the current session ID. |
| `p_request` | URL request parameter. |
| `p_debug` | URL debug parameter. Defaults to the current debug mode. |
| `p_clear_cache` | URL clear cache parameter. |
| `p_items` | Comma-delimited list of item names to set session state. |
| `p_values` | Comma-separated list of item values to set session state. |
| `p_printer_friendly` | URL printer-friendly parameter. Defaults to the current request's printer-friendly mode. |
| `p_trace` | SQL trace parameter. |
| `p_x01` | Adds the parameter `&x01=value` to the URL. |
| `p_hash` | Adds `#hash-value` at the end of the URL. |
| `p_triggering_element` | A jQuery selector to identify which element to use to trigger the dialog (for example, `#my_button`, where "my_button" is the static ID for a button element). Required for Modal Dialog support. |
| `p_plain_url` | If the page you are calling `APEX_PAGE.GET_URL` from is a modal dialog, specify `p_plain_url` to omit the unnecessary JavaScript code in the generated link. By default, if this function is called from a modal dialog, JavaScript code to close the modal dialog is included in the generated URL. |
| `p_absolute_url` | If `FALSE` (default), auto-determines if an absolute URL is needed. If `TRUE`, always generates an absolute URL. |

---

## IS_DESKTOP_UI Function (Deprecated)

Note:

This API is deprecated and will be removed in a future release.

This function returns `TRUE` if the current page has been designed for desktop browsers.

Syntax

```sql
FUNCTION IS_DESKTOP_UI
RETURN BOOLEAN;
```

---

## IS_READ_ONLY Function

This function returns `TRUE` if the current page is rendered read-only and `FALSE` if it is not.

Syntax

```sql
FUNCTION IS_READ_ONLY
RETURN BOOLEAN;
```

---

## PURGE_CACHE Procedure

This procedure purges the cache of the specified application, page, and region for the specified user. If the user is not specified, the procedure purges all cached versions of the page.

Syntax

```sql
APEX_PAGE.PURGE_CACHE (
    p_application_id       IN NUMBER DEFAULT apex.g_flow_id,
    p_page_id              IN NUMBER DEFAULT apex.g_flow_step_id,
    p_user_name            IN VARCHAR2 DEFAULT NULL,
    p_current_session_only IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | `ID` of the application. Defaults to the current application. |
| `p_page_id` | `ID` of the page. Defaults to the current page. If you pass NULL, Oracle APEX purges the cache on all pages of the application. |
| `p_user_name` | Specify a user name if you only want to purge entries that were saved for the given user. |
| `p_current_session_only` | Specify `TRUE` if you only want to purge entries that where saved for the current session. Defaults to `FALSE`. |