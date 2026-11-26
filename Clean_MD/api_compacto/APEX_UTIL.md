<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_UTIL (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_UTIL

The APEX_UTIL package provides utilities you can use when programming in the Oracle APEX environment. You can use the APEX_UTIL package to get and set session state, to get files, to check authorizations for users, to reset different states for users, to get and purge cache information, and to get and set preferences for users.

---

## BLOB_TO_CLOB Function

This function converts a BLOB to a temporary CLOB.

Syntax

```sql
APEX_UTIL.BLOB_TO_CLOB (
    p_blob              IN BLOB,
    p_charset           IN VARCHAR2 DEFAULT NULL,
    --
    p_in_memory         IN VARCHAR2 DEFAULT 'Y',
    p_free_immediately  IN VARCHAR2 DEFAULT 'Y' )
RETURN CLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_blob` | BLOB to be converted to a CLOB. |
| `p_charset` | Character set of the BLOB to be converted. If omitted, the database character set is assumed and no character set conversion happens. |
| `p_in_memory` | If `Y` is specified, create the temporary LOB in memory. |
| `p_free_immediately` | If `Y` is specified, clean up the temporary LOB after the top-level call. |

Returns

Temporary CLOB containing the BLOB contents.

---

## CACHE_GET_DATE_OF_PAGE_CACHE Function

This function returns the date and time a specified application page was cached either for the user issuing the call, or for all users if the page was not set to be cached by user.

Syntax

```sql
APEX_UTIL.CACHE_GET_DATE_OF_PAGE_CACHE (
    p_application  IN NUMBER,
    p_page         IN NUMBER )
RETURN DATE;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application` | The identification number (ID) of the application. |
| `p_page` | The page number (ID). |

---

## CACHE_GET_DATE_OF_REGION_CACHE Function

This function returns the date and time a specified region was cached either for the user issuing the call, or for all users if the page was not set to be cached by user.

Syntax

```sql
APEX_UTIL.CACHE_GET_DATE_OF_REGION_CACHE (
    p_application  IN NUMBER,
    p_page         IN NUMBER,
    p_region_name  IN VARCHAR2 )
RETURN DATE;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application` | The identification number (ID) of the application. |
| `p_page` | The page number (ID). |
| `p_region_name` | The region name. |

---

## CACHE_PURGE_BY_APPLICATION Procedure

This procedure purges all cached pages and regions for a given application.

Syntax

```sql
APEX_UTIL.CACHE_PURGE_BY_APPLICATION (
    p_application  IN NUMBER );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application` | The identification number (ID) of the application. |

---

## CACHE_PURGE_BY_PAGE Procedure

This procedure purges the cache for a given application and page. If the page itself is not cached but contains one or more cached regions, then the cache for these is also purged.

Syntax

```sql
APEX_UTIL.CACHE_PURGE_BY_PAGE (
    p_application  IN NUMBER,
    p_page         IN NUMBER,
    p_user_name    IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application` | The identification number (ID) of the application. |
| `p_page` | The page number (ID). |
| `p_user_name` | The user associated with cached pages and regions. |

---

## CACHE_PURGE_STALE Procedure

This procedure deletes all cached pages and regions for a specified application that have passed the defined active time period. When you cache a page or region, you specify an active time period (or Cache Timeout). Once that period has passed, the cache is no longer used, thus removing those unusable pages or regions from the cache.

Syntax

```sql
APEX_UTIL.CACHE_PURGE_STALE (
    p_application  IN NUMBER );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application` | The identification number (ID) of the application. |

---

## CHANGE_CURRENT_USER_PW Procedure

This procedure changes the password of the currently authenticated user.

Note:

This procedure operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.CHANGE_CURRENT_USER_PW (
    p_new_password  IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_new_password` | The new password value in clear text. |

---

## CHANGE_PASSWORD_ON_FIRST_USE Function

This function enables a developer to check whether this property is enabled or disabled for an end user account.

This function returns `TRUE` if the account password must be changed upon first use (after successful authentication) after the password is initially set and after it is changed on the Administration Service, Edit User page. This function returns `FALSE` if the account does not have this property.

This function may be run in a page request context by any authenticated user.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.CHANGE_PASSWORD_ON_FIRST_USE (
    p_user_name     IN VARCHAR2 )
RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## CLOB_TO_BLOB Function

This function converts a CLOB to a temporary BLOB.

Syntax

```sql
APEX_UTIL.CLOB_TO_BLOB (
    p_clob              IN CLOB,
    p_charset           IN VARCHAR2 DEFAULT NULL,
    p_include_bom       IN VARCHAR2 DEFAULT 'N',
    --
    p_in_memory         IN VARCHAR2 DEFAULT 'Y',
    p_free_immediately  IN VARCHAR2 DEFAULT 'Y' )
RETURN BLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_clob` | CLOB to convert to a BLOB. |
| `p_charset` | Character set to convert the BLOB to. If omitted, no character set conversion happens. |
| `p_include_bom` | Prepend the generated BLOB with a BOM. |
| `p_in_memory` | If `Y` is specified, create the temporary LOB in memory. |
| `p_free_immediately` | If `Y` is specified, clean up the temporary LOB after the top-level call. |

Returns

Temporary BLOB containing the CLOB contents.

---

## CLOSE_OPEN_DB_LINKS Procedure

This procedure closes all open database links for the current database session.

It is rare for this procedure to be called programatically in an application. The primary purpose of this procedure is for the middleware technology in an Oracle APEX environment (such as Oracle REST Data Service) to be configured such that it closes all of the open database links in a session, either before a request is made to the APEX engine, or after a request to the APEX engine is completed but before the database session is returned to the pool.

Syntax

```sql
APEX_UTIL.CLOSE_OPEN_DB_LINKS
```

Parameters

None.

---

## CLEAR_APP_CACHE Procedure

This procedure removes session state for a given application for the current session.

Syntax

```sql
APEX_UTIL.CLEAR_APP_CACHE (
    p_app_id    IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_app_id` | The ID of the application for which session state is cleared for current session. |

---

## CLEAR_PAGE_CACHE Procedure

This procedure removes session state for a given page for the current session. If `p_page_id` is not specified, then the current page will be cleared.

Syntax

```sql
APEX_UTIL.CLEAR_PAGE_CACHE (
    p_page_id IN NUMBER DEFAULT NULL);
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_page_id` | The ID of the page in the current application for which session state is cleared for current session. |

---

## CLEAR_USER_CACHE Procedure

This procedure removes session state and application system preferences for the current user's session. Run this procedure if you reuse session IDs and want to run applications without the benefit of existing session state.

Syntax

```sql
APEX_UTIL.CLEAR_USER_CACHE;
```

Parameters

None.

---

## COUNT_CLICK Procedure

This procedure counts clicks from an application built in App Builder to an external site. You can also use the shorthand version, procedure `Z`, in place of `APEX_UTIL.COUNT_CLICK`.

Syntax

```sql
APEX_UTIL.COUNT_CLICK (
    p_url             IN VARCHAR2,
    p_cat             IN VARCHAR2,
    p_id              IN VARCHAR2 DEFAULT NULL,
    p_user            IN VARCHAR2 DEFAULT NULL,
    p_workspace       IN VARCHAR2 DEFAULT NULL,
    p_referrer_policy IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_url` | The URL to which to redirect. |
| `p_cat` | A category to classify the click. |
| `p_id` | (Optional) Secondary ID to associate with the click. |
| `p_user` | (Optional) The application user ID. |
| `p_workspace` | (Optional) The workspace associated with the application. |
| `p_referrer_policy` | The referrer-policy HTTP response header. |

---

## CREATE_USER Procedure

This procedure creates a new account record in the native Oracle APEX user accounts repository.

Use this procedure to programmatically create user accounts for applications that utilize the APEX Accounts authentication scheme. To execute this procedure within the context of an APEX application, the current user must be an APEX workspace administrator and the application must permit modification of the workspace repository.

When creating workspace developer or workspace administrator users, you must also ensure that the user can authenticate to the development environment authentication scheme. The CREATE_USER procedure only creates the APEX repository user. For example, if using Database Accounts authentication, you must also run `CREATE USER nnn IDENTIFIED BY yyy`.

Syntax

```sql
APEX_UTIL.CREATE_USER (
    p_user_id                       IN NUMBER   DEFAULT NULL,
    p_user_name                     IN VARCHAR2,
    p_first_name                    IN VARCHAR2 DEFAULT NULL,
    p_last_name                     IN VARCHAR2 DEFAULT NULL,
    p_description                   IN VARCHAR2 DEFAULT NULL,
    p_email_address                 IN VARCHAR2 DEFAULT NULL,
    p_web_password                  IN VARCHAR2,
    p_web_password_format           IN VARCHAR2 DEFAULT 'CLEAR_TEXT',
    p_group_ids                     IN VARCHAR2 DEFAULT NULL,
    p_developer_privs               IN VARCHAR2 DEFAULT NULL,
    p_default_schema                IN VARCHAR2 DEFAULT NULL,
    p_default_date_format           IN VARCHAR2 DEFAULT NULL,
    p_allow_access_to_schemas       IN VARCHAR2 DEFAULT NULL,
    p_account_expiry                IN DATE     DEFAULT TRUNC(SYSDATE),
    p_account_locked                IN VARCHAR2 DEFAULT 'N',
    p_failed_access_attempts        IN NUMBER   DEFAULT 0,
    p_change_password_on_first_use  IN VARCHAR2 DEFAULT 'Y',
    p_first_password_use_occurred   IN VARCHAR2 DEFAULT 'N',
    p_attribute_01                  IN VARCHAR2 DEFAULT NULL,
    p_attribute_02                  IN VARCHAR2 DEFAULT NULL,
    p_attribute_03                  IN VARCHAR2 DEFAULT NULL,
    p_attribute_04                  IN VARCHAR2 DEFAULT NULL,
    p_attribute_05                  IN VARCHAR2 DEFAULT NULL,
    p_attribute_06                  IN VARCHAR2 DEFAULT NULL,
    p_attribute_07                  IN VARCHAR2 DEFAULT NULL,
    p_attribute_08                  IN VARCHAR2 DEFAULT NULL,
    p_attribute_09                  IN VARCHAR2 DEFAULT NULL,
    p_attribute_10                  IN VARCHAR2 DEFAULT NULL,
    p_allow_app_building_yn         IN VARCHAR2 DEFAULT NULL,
    p_allow_sql_workshop_yn         IN VARCHAR2 DEFAULT NULL,
    p_allow_websheet_dev_yn         IN VARCHAR2 DEFAULT NULL,
    p_allow_team_development_yn     IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_id` | Numeric primary key of user account. |
| `p_user_name` | Alphanumeric name used for login. |
| `p_first_name` | Informational. |
| `p_last_name` | Informational. |
| `p_description` | Informational. |
| `p_email_address` | Email address. |
| `p_web_password` | Password. |
| `p_web_password_format` | If the value you are passing for the `p_web_password` parameter is in clear text format then use `CLEAR_TEXT`, otherwise use `HEX_ENCODED_DIGEST_V2`. |
| `p_group_ids` | Colon separated list of numeric group IDs. |
| `p_developer_privs` | Colon separated list of developer privileges. If `p_developer_privs` is not null, the user is given access to Team Development. If `p_developer_privs` contains `ADMIN`, the user is given App Builder and SQL Workshop access. If `p_developer_privs` does not contain ADMIN but contains `EDIT`, the user is given App Builder access. If `p_developer_privs` does not contain ADMIN but contains `SQL`, the user is given SQL Workshop access.  The following are acceptable values for this parameter:  `NULL` - To create an end user (a user who can only authenticate to developed applications).  `CREATE:DATA_LOADER:EDIT:HELP:MONITOR:SQL` - To create a user with developer privileges with access to App Builder and SQL Workshop.  `ADMIN:CREATE:DATA_LOADER:EDIT:HELP:MONITOR:SQL` - To create a user with full workspace administrator and developer privileges with access to App Builder, SQL Workshop and Team Development.  Note: Currently this parameter is named inconsistently between the `CREATE_USER`, `EDIT_USER`, and `FETCH_USER` APIs, although they all relate to the `DEVELOPER_ROLE` field stored in the named user account record. `CREATE_USER` uses `p_developer_privs`; `EDIT_USER` uses `p_developer_roles`; and `FETCH_USER` uses `p_developer_role`. |
| `p_default_schema` | A database schema assigned to the user's workspace, used by default for browsing. |
| `p_default_date_format` | Oracle Date format for user. Currently only used in SQL Workshop. |
| `p_allow_access_to_schemas` | Colon-separated list of schemas assigned to the user's workspace to which the user is restricted (leave NULL for all). |
| `p_account_expiry` | The date the password was last updated, which defaults to today's date on creation. |
| `p_account_locked` | `Y` or `N` indicating if account is locked or unlocked. |
| `p_failed_access_attempts` | Number of consecutive login failures that have occurred, defaults to `0` on creation. |
| `p_change_password_on_first_use` | `Y` or `N` to indicate whether password must be changed on first use, defaults to `Y` on creation. |
| `p_first_password_use_occurred` | `Y` or `N` to indicate whether login has occurred since password change, defaults to `N` on creation. |
| `p_attribute_01` … `p_attribute_10` | Arbitrary text accessible with an API. |
| `p_allow_app_building_yn` | `Y` or `N` to indicate whether access to App Builder is enabled. |
| `p_allow_sql_workshop_yn` | `Y` or `N` to indicate whether access to SQL Workshop is enabled.. |
| `p_allow_websheet_dev_yn` | `Y` or `N` to indicate whether access to Websheet development is enabled. |
| `p_allow_team_development_yn` | `Y` or `N` to indicate whether access to Team Development is enabled. |

---

## CREATE_USER_GROUP Procedure

This procedure creates a user group when you are using Oracle APEX Accounts authentication.

To execute this procedure within the context of an APEX application, the current user must be an APEX workspace administrator and the application must permit modification of the workspace repository.

Note:

This procedure operates on the native APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.CREATE_USER_GROUP (
    p_id                    IN NUMBER   DEFAULT NULL,
    p_group_name            IN VARCHAR2,
    p_security_group_id     IN NUMBER   DEFAULT NULL,
    p_group_desc            IN VARCHAR2 DEFAULT NULL );
```

Parameter

| Parameter | Description |
| --- | --- |
| `p_id` | Primary key of group. |
| `p_group_name` | Name of group. |
| `p_security_group_id` | Workspace ID. |
| `p_group_desc` | Descriptive text. |

---

## CURRENT_USER_IN_GROUP Function

This function returns a Boolean result based on whether the current user is a member of the specified workspace group. You can use the group name or group ID to identify the group.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.CURRENT_USER_IN_GROUP (
    p_group_name  IN VARCHAR2 )
RETURN BOOLEAN;

APEX_UTIL.CURRENT_USER_IN_GROUP (
    p_group_id    IN NUMBER )
RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_group_name` | Identifies the name of an existing group in the workspace. |
| `p_group_id` | Identifies the numeric ID of an existing group in the workspace. |

---

## CUSTOM_CALENDAR Procedure (Deprecated)

Note:

This API is deprecated and will be
removed in a future release.

Use this procedure to change the existing calendar view to Custom Calendar.

Syntax

```sql
APEX_UTIL.CUSTOM_CALENDAR(
    p_date_type_field IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_date_type_field` | Identifies the item name used to define the type of calendar to be displayed. |

---

## DELETE_FEEDBACK Procedure

This procedure deletes feedback with the specified ID.

Syntax

```sql
APEX_UTIL.DELETE_FEEDBACK (
    p_feedback_id      IN NUMBER )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_feedback_id` | The ID of the feedback. |

---

## DELETE_FEEDBACK_ATTACHMENT Procedure

This procedure deletes the attachment of a feedback with the specified ID.

Syntax

```sql
APEX_UTIL.DELETE_FEEDBACK_ATTACHMENT (
    p_feedback_id      IN NUMBER )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_feedback_id` | The ID of the feedback. |

---

## DELETE_USER_GROUP Procedure Signature 1

This procedure deletes a user group by providing the primary key of the group when you are using Oracle APEX Accounts authentication. To execute this procedure, the current user must have administrative privileges in the workspace.

Note:

This procedure operates on the native APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.DELETE_USER_GROUP (
    p_group_id  IN NUMBER );
```

Parameter

| Parameter | Description |
| --- | --- |
| `p_group_id` | Primary key of group. |

---

## DELETE_USER_GROUP Procedure Signature 2

This procedure deletes a user group by providing the name of the group when you are using Oracle APEX Accounts authentication. To execute this procedure, the current user must have administrative privileges in the workspace.

Note:

This procedure operates on the native APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.DELETE_USER_GROUP (
    p_group_name    IN VARCHAR2 );
```

Parameter

| Parameter | Description |
| --- | --- |
| `p_group_name` | Name of group. |

---

## DOWNLOAD_PRINT_DOCUMENT Procedure Signature 1

This procedure initiates the download of a print document using XML based report data (as a BLOB) and RTF or XSL-FO based report layout.

Syntax

```sql
APEX_UTIL.DOWNLOAD_PRINT_DOCUMENT (
    p_file_name           IN VARCHAR,
    p_content_disposition IN VARCHAR  DEFAULT 'attachment',
    p_report_data         IN BLOB,
    p_report_layout       IN CLOB,
    p_report_layout_type  IN VARCHAR2 DEFAULT 'xsl-fo',
    p_document_format     IN VARCHAR2 DEFAULT 'pdf',
    p_print_server        IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_file_name` | Defines the filename of the print document. |
| `p_content_disposition` | Specifies whether to download the print document or display inline ("attachment", "inline"). |
| `p_report_data` | XML based report data. |
| `p_report_layout` | Report layout in XSL-FO or RTF format. |
| `p_report_layout_type` | Defines the report layout type, that is "xsl-fo" or "rtf". |
| `p_document_format` | Defines the document format, that is "pdf", "rtf", "xls", "htm", or "xml". |
| `p_print_server` | URL of the print server. If not specified, the print server is derived from preferences. |

See Also:

Printing Report Regions in Oracle APEX App Builder
User’s Guide

---

## DOWNLOAD_PRINT_DOCUMENT Procedure Signature 2

This procedure initiates the download of a print document using a pre-defined report query and an RTF or XSL-FO based report layout.

Syntax

```sql
APEX_UTIL.DOWNLOAD_PRINT_DOCUMENT (
    p_file_name           IN VARCHAR,
    p_content_disposition IN VARCHAR  DEFAULT 'attachment',
    p_application_id      IN NUMBER,
    p_report_query_name   IN VARCHAR2,
    p_report_layout       IN CLOB,
    p_report_layout_type  IN VARCHAR2 DEFAULT 'xsl-fo',
    p_document_format     IN VARCHAR2 DEFAULT 'pdf',
    p_print_server        IN VARCHAR2 DEFAULT NULL);
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_file_name` | Defines the filename of the print document. |
| `p_content_disposition` | Specifies whether to download the print document or display inline ("attachment", "inline"). |
| `p_application_id` | Defines the application ID of the report query. |
| `p_report_query_name` | Name of the report query (stored under application's Shared Components). |
| `p_report_layout` | Report layout in XSL-FO or RTF format. |
| `p_report_layout_type` | Defines the report layout type, that is "xsl-fo" or "rtf". |
| `p_document_format` | Defines the document format, that is "pdf", "rtf", "xls", "htm", or "xml". |
| `p_print_server` | URL of the print server. If not specified, the print server is derived from preferences. |

---

## DOWNLOAD_PRINT_DOCUMENT Procedure Signature 3

This procedure initiates the download of a print document using pre-defined report query and pre-defined report layout.

Syntax

```sql
APEX_UTIL.DOWNLOAD_PRINT_DOCUMENT (
    p_file_name           IN VARCHAR,
    p_content_disposition IN VARCHAR  DEFAULT 'attachment',
    p_application_id      IN NUMBER,
    p_report_query_name   IN VARCHAR2,
    p_report_layout_name  IN VARCHAR2,
    p_report_layout_type  IN VARCHAR2 DEFAULT 'xsl-fo',
    p_document_format     IN VARCHAR2 DEFAULT 'pdf',
    p_print_server        IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_file_name` | Defines the filename of the print document. |
| `p_content_disposition` | Specifies whether to download the print document or display inline ("attachment", "inline"). |
| `p_application_id` | Defines the application ID of the report query. |
| `p_report_query_name` | Name of the report query (stored under application's Shared Components). |
| `p_report_layout_name` | Name of the report layout (stored under application's Shared Components). |
| `p_report_layout_type` | Defines the report layout type, that is "xsl-fo" or "rtf". |
| `p_document_format` | Defines the document format, that is "pdf", "rtf", "xls", "htm", or "xml". |
| `p_print_server` | URL of the print server. If not specified, the print server is derived from preferences. |

---

## DOWNLOAD_PRINT_DOCUMENT Procedure Signature 4

This procedure initiates the download of a print document using XML based report data (as a CLOB) and RTF or XSL-FO based report layout.

Syntax

```sql
APEX_UTIL.DOWNLOAD_PRINT_DOCUMENT (
    p_file_name           IN VARCHAR,
    p_content_disposition IN VARCHAR,
    p_report_data         IN CLOB,
    p_report_layout       IN CLOB,
    p_report_layout_type  IN VARCHAR2 DEFAULT 'xsl-fo',
    p_document_format     IN VARCHAR2 DEFAULT 'pdf',
    p_print_server        IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_file_name` | Defines the filename of the print document. |
| `p_content_disposition` | Specifies whether to download the print document or display inline ("attachment", "inline"). |
| `p_report_data` | XML based report data, must be encoded in UTF-8. |
| `p_report_layout` | Report layout in XSL-FO or RTF format. |
| `p_report_layout_type` | Defines the report layout type, that is "xsl-fo" or "rtf". |
| `p_document_format` | Defines the document format, that is "pdf", "rtf", "xls", "htm", or "xml". |
| `p_print_server` | URL of the print server. If not specified, the print server is derived from preferences. |

---

## EDIT_USER Procedure

This procedure enables a user account record to be altered. To execute this procedure, the current user must have administrative privileges in the workspace.

Syntax

```sql
APEX_UTIL.EDIT_USER (
    p_user_id                      IN                   NUMBER,
    p_user_name                    IN                   VARCHAR2,
    p_first_name                   IN                   VARCHAR2    DEFAULT NULL,
    p_last_name                    IN                   VARCHAR2    DEFAULT NULL,
    p_web_password                 IN                   VARCHAR2    DEFAULT NULL,
    p_new_password                 IN                   VARCHAR2    DEFAULT NULL,
    p_email_address                IN                   VARCHAR2    DEFAULT NULL,
    p_start_date                   IN                   VARCHAR2    DEFAULT NULL,
    p_end_date                     IN                   VARCHAR2    DEFAULT NULL,
    p_employee_id                  IN                   VARCHAR2    DEFAULT NULL,
    p_allow_access_to_schemas      IN                   VARCHAR2    DEFAULT NULL,
    p_person_type                  IN                   VARCHAR2    DEFAULT NULL,
    p_default_schema               IN                   VARCHAR2    DEFAULT NULL,
    p_group_ids                    IN                   VARCHAR2    DEFAULT NULL,
    p_developer_roles              IN                   VARCHAR2    DEFAULT NULL,
    p_description                  IN                   VARCHAR2    DEFAULT NULL,
    p_account_expiry               IN                   DATE        DEFAULT NULL,
    p_account_locked               IN                   VARCHAR2    DEFAULT 'N',
    p_failed_access_attempts       IN                   NUMBER      DEFAULT 0,
    p_change_password_on_first_use IN                   VARCHAR2    DEFAULT 'Y',
    p_first_password_use_occurred  IN                   VARCHAR2    DEFAULT 'N');
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_id` | Numeric primary key of the user account. |
| `p_user_name` | Alphanumeric name used for login.  See also SET_USERNAME Procedure |
| `p_first_name` | Informational.  See also SET_FIRST_NAME Procedure |
| `p_last_name` | Informational.  See also SET_LAST_NAME Procedure |
| `p_web_password` | Clear text password. If using this procedure to update the password for the user, values for both `p_web_password` and `p_new_password` must not be null and must be identical. |
| `p_new_password` | Clear text new password. If using this procedure to update the password for the user, values for both `p_web_password` and `p_new_password` must not be null and must be identical. |
| `p_email_address` | Informational.  See also SET_EMAIL Procedure |
| `p_start_date` | Unused. |
| `p_end_date` | Unused. |
| `p_employee_id` | Unused. |
| `p_allow_access_to_schemas` | A list of schemas assigned to the user's workspace to which the user is restricted. |
| `p_person_type` | Unused. |
| `p_default_schema` | A database schema assigned to the user's workspace, used by default for browsing. |
| `p_group_ids` | Colon-separated list of numeric group IDs. |
| `p_developer_roles` | Colon-separated list of developer privileges. The following are acceptable values for this parameter:   * null - To update the user to be an end user (a user who can only authenticate to developed applications). * CREATE:DATA_LOADER:EDIT:HELP:MONITOR:SQL - To update the user to have developer privilege. * ADMIN:CREATE:DATA_LOADER:EDIT:HELP:MONITOR:SQL - To update the user to have full workspace administrator and developer privilege.   Note: Currently this parameter is named inconsistently between the CREATE_USER, EDIT_USER and FETCH_USER APIs, although they all relate to the DEVELOPER_ROLE field stored in the named user account record. CREATE_USER uses p_developer_privs, EDIT_USER uses p_developer_roles and FETCH_USER uses p_developer_role.  See also GET_USER_ROLES Function |
| `p_description` | Informational. |
| `p_account_expiry` | Date password was last updated.  See also:  * EXPIRE_END_USER_ACCOUNT Procedure * EXPIRE_WORKSPACE_ACCOUNT Procedure * UNEXPIRE_END_USER_ACCOUNT Procedure * UNEXPIRE_WORKSPACE_ACCOUNT Procedure |
| `p_account_locked` | 'Y' or 'N' indicating if account is locked or unlocked.  See also:  * LOCK_ACCOUNT Procedure * UNLOCK_ACCOUNT Procedure |
| `p_failed_access_attempts` | Number of consecutive login failures that have occurred. |
| `p_change_password_on_first_use` | 'Y' or 'N' to indicate whether password must be changed on first use.  See also CHANGE_PASSWORD_ON_FIRST_USE Function |
| `p_first_password_use_occurred` | 'Y' or 'N' to indicate whether login has occurred since password change.  See also PASSWORD_FIRST_USE_OCCURRED Function |

---

## END_USER_ACCOUNT_DAYS_LEFT Function

This function returns the number of days remaining before an end user account password expires. This function may be run in a page request context by any authenticated user.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.END_USER_ACCOUNT_DAYS_LEFT (
    p_user_name     IN VARCHAR2 );
RETURN NUMBER
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## EXPIRE_END_USER_ACCOUNT Procedure

This procedure expires the login account for use as a workspace end user. Must be run by an authenticated workspace administrator in a page request context.

Note:

This procedure operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.EXPIRE_END_USER_ACCOUNT (
    p_user_name     IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## EXPIRE_WORKSPACE_ACCOUNT Procedure

This procedure expires developer or workspace administrator login accounts. Must be run by an authenticated workspace administrator in a page request context.

Syntax

```sql
APEX_UTIL.EXPIRE_WORKSPACE_ACCOUNT (
    p_user_name IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## EXPORT_USERS Procedure

This procedure produces an export file of the current workspace definition, workspace users, and workspace groups when called from a page. To execute this procedure, the current user must have administrative privilege in the workspace.

Syntax

```sql
APEX_UTIL.EXPORT_USERS (
    p_export_format     IN VARCHAR2 DEFAULT 'UNIX' );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_export_format` | Indicates how rows in the export file are formatted. Specify `UNIX` to have the resulting file contain rows delimited by line feeds. Specify `DOS` to have the resulting file contain rows delimited by carriage returns and line feeds. |

---

## FEEDBACK_ENABLED Function

This function returns a boolean value to check if application feature Allow Feedback
is enabled.

Syntax

```sql
APEX_UTIL.FEEDBACK_ENABLED
    RETURN boolean;
```

Parameters

None.

---

## FETCH_APP_ITEM Function

This function fetches session state for the current or specified application in the current or specified session.

Syntax

```sql
APEX_UTIL.FETCH_APP_ITEM (
    p_item    IN VARCHAR2,
    p_app     IN NUMBER DEFAULT NULL,
    p_session IN NUMBER DEFAULT NULL )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_item` | The name of an application-level item (not a page item) whose current value is to be fetched. |
| `p_app` | The ID of the application that owns the item (leave null for the current application). |
| `p_session` | The session ID from which to obtain the value (leave null for the current session). |

---

## FETCH_USER Procedure Signature 1

This procedure fetches a user account record. To execute this procedure, the current user must have administrative privileges in the workspace. Three overloaded versions of this procedure exist, each with a distinct set of allowed parameters or signatures.

Note:

This procedure operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.FETCH_USER (
    p_user_id                       IN                    NUMBER,
    p_workspace                     OUT                   VARCHAR2,
    p_user_name                     OUT                   VARCHAR2,
    p_first_name                    OUT                   VARCHAR2,
    p_last_name                     OUT                   VARCHAR2,
    p_web_password                  OUT                   VARCHAR2,
    p_email_address                 OUT                   VARCHAR2,
    p_start_date                    OUT                   VARCHAR2,
    p_end_date                      OUT                   VARCHAR2,
    p_employee_id                   OUT                   VARCHAR2,
    p_allow_access_to_schemas       OUT                   VARCHAR2,
    p_person_type                   OUT                   VARCHAR2,
    p_default_schema                OUT                   VARCHAR2,
    p_groups                        OUT                   VARCHAR2,
    p_developer_role                OUT                   VARCHAR2,
    p_description                   OUT                   VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_id` | Numeric primary key of the user account. |
| `p_workspace` | The name of the workspace. |
| `p_user_name` | Alphanumeric name used for login.  See also GET_USERNAME Function |
| `p_first_name` | Informational.  See also GET_FIRST_NAME Function |
| `p_last_name` | Informational.  See also GET_LAST_NAME Function |
| `p_web_password` | Obfuscated account password. |
| `p_email_address` | Email address.  See also GET_EMAIL Function |
| `p_start_date` | Unused. |
| `p_end_date` | Unused. |
| `p_employee_id` | Unused. |
| `p_allow_access_to_schemas` | A list of schemas assigned to the user's workspace to which user is restricted. |
| `p_person_type` | Unused. |
| `p_default_schema` | A database schema assigned to the user's workspace, used by default for browsing.  See also GET_DEFAULT_SCHEMA Function |
| `p_groups` | List of groups of which user is a member.  See also  * GET_GROUPS_USER_BELONGS_TO Function * CURRENT_USER_IN_GROUP Function |
| `p_developer_role` | Colon-separated list of developer roles. The following are acceptable values for this parameter:  `null` - Indicates an end user (a user who can only authenticate to developed applications).  `CREATE:DATA_LOADER:EDIT:HELP:MONITOR:SQL` - Indicates a user with developer privilege.  `ADMIN:CREATE:DATA_LOADER:EDIT:HELP:MONITOR:SQL` - Indicates a user with full workspace administrator and developer privilege.  Note: Currently this parameter is named inconsistently between the `CREATE_USER`, `EDIT_USER` and `FETCH_USER` APIs, although they all relate to the `DEVELOPER_ROLE` field stored in the named user account record. `CREATE_USER` uses `p_developer_privs`, `EDIT_USER` uses `p_developer_roles` and `FETCH_USER` uses `p_developer_role`.  See also GET_USER_ROLES Function |
| `p_description` | Informational. |

---

## FETCH_USER Procedure Signature 2

This procedure fetches a user account record. To execute this procedure, the current user must have administrative privileges in the workspace. Three overloaded versions of this procedure exist, each with a distinct set of allowed parameters or signatures.

Note:

This procedure operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.FETCH_USER (
    p_user_id                     IN                 NUMBER,
    p_user_name                   OUT                VARCHAR2,
    p_first_name                  OUT                VARCHAR2,
    p_last_name                   OUT                VARCHAR2,
    p_email_address               OUT                VARCHAR2,
    p_groups                      OUT                VARCHAR2,
    p_developer_role              OUT                VARCHAR2,
    p_description                 OUT                VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_id` | Numeric primary key of the user account. |
| `p_user_name` | Alphanumeric name used for login.  See also GET_USERNAME Function |
| `p_first_name` | Informational. See also GET_FIRST_NAME Function |
| `p_last_name` | Informational.  See also GET_LAST_NAME Function |
| `p_email_address` | Email address.  See also GET_EMAIL Function |
| `p_groups` | List of groups of which user is a member.  See also  * GET_GROUPS_USER_BELONGS_TO Function * CURRENT_USER_IN_GROUP Function |
| `p_developer_role` | Colon-separated list of developer roles. The following are acceptable values for this parameter:  `null` - Indicates an end user (a user who can only authenticate to developed applications).  `CREATE:DATA_LOADER:EDIT:HELP:MONITOR:SQL` - Indicates a user with developer privilege.  `ADMIN:CREATE:DATA_LOADER:EDIT:HELP:MONITOR:SQL` - Indicates a user with full workspace administrator and developer privilege.  Note: Currently this parameter is named inconsistently between the `CREATE_USER`, `EDIT_USER` and `FETCH_USER` APIs, although they all relate to the `DEVELOPER_ROLE` field stored in the named user account record. `CREATE_USER` uses `p_developer_privs`, `EDIT_USER` uses `p_developer_roles` and `FETCH_USER` uses `p_developer_role`.  See also GET_USER_ROLES Function |
| `p_description` | Informational. |

---

## FETCH_USER Procedure Signature 3

This procedure fetches a user account record. To execute this procedure, the current user must have administrative privileges in the workspace. Three overloaded versions of this procedure exist, each with a distinct set of allowed parameters or signatures.

Note:

This procedure operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.FETCH_USER (
    p_user_id                           IN                   NUMBER,
    p_workspace                         OUT                  VARCHAR2,
    p_user_name                         OUT                  VARCHAR2,
    p_first_name                        OUT                  VARCHAR2,
    p_last_name                         OUT                  VARCHAR2,
    p_web_password                      OUT                  VARCHAR2,
    p_email_address                     OUT                  VARCHAR2,
    p_start_date                        OUT                  VARCHAR2,
    p_end_date                          OUT                  VARCHAR2,
    p_employee_id                       OUT                  VARCHAR2,
    p_allow_access_to_schemas           OUT                  VARCHAR2,
    p_person_type                       OUT                  VARCHAR2,
    p_default_schema                    OUT                  VARCHAR2,
    p_groups                            OUT                  VARCHAR2,
    p_developer_role                    OUT                  VARCHAR2,
    p_description                       OUT                  VARCHAR2,
    p_account_expiry                    OUT                  DATE,
    p_account_locked                    OUT                  VARCHAR2,
    p_failed_access_attempts            OUT                  NUMBER,
    p_change_password_on_first_use      OUT                  VARCHAR2,
    p_first_password_use_occurred       OUT                  VARCHAR2 );
```

Parameters

Table 59-1 Fetch_User Parameters Signature 3

| Parameter | Description |
| --- | --- |
| `p_user_id` | Numeric primary key of the user account. |
| `p_workspace` | The name of the workspace. |
| `p_user_name` | Alphanumeric name used for login.  See also GET_USERNAME Function |
| `p_first_name` | Informational.  See also GET_FIRST_NAME Function |
| `p_last_name` | Informational.  See also GET_LAST_NAME Function |
| `p_web_password` | Obfuscated account password. |
| `p_email_address` | Email address.  See also GET_EMAIL Function |
| `p_start_date` | Unused. |
| `p_end_date` | Unused. |
| `p_employee_id` | Unused. |
| `p_allow_access_to_schemas` | A list of schemas assigned to the user's workspace to which user is restricted. |
| `p_person_type` | Unused. |
| `p_default_schema` | A database schema assigned to the user's workspace, used by default for browsing.  See also GET_DEFAULT_SCHEMA Function |
| `p_groups` | List of groups of which user is a member.  See also  * GET_GROUPS_USER_BELONGS_TO Function * CURRENT_USER_IN_GROUP Function |
| `p_developer_role` | Colon-separated list of developer roles. The following are acceptable values for this parameter:  `null` - Indicates an end user (a user who can only authenticate to developed applications).  `CREATE:DATA_LOADER:EDIT:HELP:MONITOR:SQL` - Indicates a user with developer privilege.  `ADMIN:CREATE:DATA_LOADER:EDIT:HELP:MONITOR:SQL` - Indicates a user with full workspace administrator and developer privilege.  Note: Currently this parameter is named inconsistently between the `CREATE_USER`, `EDIT_USER` and `FETCH_USER` APIs, although they all relate to the `DEVELOPER_ROLE` field stored in the named user account record. `CREATE_USER` uses `p_developer_privs`, `EDIT_USER` uses `p_developer_roles` and `FETCH_USER` uses `p_developer_role`.  See also GET_USER_ROLES Function |
| `p_description` | Informational. |
| `p_account_expiry` | Date account password was last reset.  See also  * END_USER_ACCOUNT_DAYS_LEFT Function * WORKSPACE_ACCOUNT_DAYS_LEFT Function |
| `p_account_locked` | Locked/Unlocked indicator `Y` or `N`.  See also GET_ACCOUNT_LOCKED_STATUS Function |
| `p_failed_access_attempts` | Counter for consecutive login failures. |
| `p_change_password_on_first_use` | Setting to force password change on first use `Y` or `N`. |
| `p_first_password_use_occurred` | Indicates whether login with password occurred `Y` or `N`. |

---

## FIND_SECURITY_GROUP_ID Function

This function returns the numeric security group ID of the named workspace.

Syntax

```sql
APEX_UTIL.FIND_SECURITY_GROUP_ID (
    p_workspace    IN VARCHAR2 )
RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_workspace` | The name of the workspace. |

---

## FIND_WORKSPACE Function

This function returns the workspace name associated with a security group ID.

Syntax

```sql
APEX_UTIL.FIND_WORKSPACE (
    p_security_group_id    IN VARCHAR2 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_security_group_id` | The security group ID of a workspace. |

---

## GET_ACCOUNT_LOCKED_STATUS Function

This function returns `TRUE` if the account is locked and `FALSE` if the account is unlocked. Must be run by an authenticated workspace administrator in a page request context.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.GET_ACCOUNT_LOCKED_STATUS (
    p_user_name     IN VARCHAR2 )
    RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## GET_APEX_OWNER Function

This function returns the name of the schema containing the Oracle APEX engine.

Syntax

```sql
APEX_UTIL.GET_APEX_OWNER RETURN VARCHAR2;
```

Parameters

None.

Returns

The schema name which contains the APEX engine.

---

## GET_APPLICATION_STATUS Function (Deprecated)

Note:

This API is deprecated and will be removed in a future release.

Use GET_APPLICATION_STATUS Function in APEX_APPLICATION_ADMIN instead.

This function returns the current status of the application. Status values include `AVAILABLE`, `AVAILABLE_W_EDIT_LINK`, `DEVELOPERS_ONLY`, `RESTRICTED_ACCESS`, `UNAVAILABLE`, `UNAVAILABLE_PLSQL`, and `UNAVAILABLE_URL`.

Syntax

```sql
APEX_UTIL.GET_APPLICATION_STATUS (
    p_application_id IN NUMBER ) RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The application ID. |

---

## GET_ATTRIBUTE Function

This function returns the value of one of the attribute values (1 through 10) of a named user in the Oracle APEX accounts table. These are only accessible by using the APIs.

Syntax

```sql
APEX_UTIL.GET_ATTRIBUTE (
    p_username                IN VARCHAR2,
    p_attribute_number        IN NUMBER )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | User name in the account. |
| `p_attribute_number` | Number of attributes in the user record (1 through 10). |

---

## GET_AUTHENTICATION_RESULT Function

Use this function to retrieve the authentication result of the current session. Any authenticated user can call this function in a page request context.

Syntax

```sql
APEX_UTIL.GET_AUTHENTICATION_RESULT
RETURN NUMBER;
```

Parameters

None.

---

## GET_BLOB_FILE_SRC Function

As an alternative to using the built-in methods of providing a download link, you can use the `APEX_UTIL.GET_BLOB_FILE_SRC` function. One advantage of this approach is more specific formatting of the display of the image (with height and width tags). This function must be called from a valid Oracle APEX session and also requires that the parameters that describe the BLOB are listed as the format of a valid item within the application. That item is then referenced by the function.

If the URL returned by this function is passed to `APEX_UTIL.PREPARE_URL`, the `p_plain_url` argument must be set to `TRUE` to ensure that no modal dialog code is added when the referenced page item is on a modal page.

Syntax

```sql
APEX_UTIL.GET_BLOB_FILE_SRC (
    p_item_name           IN VARCHAR2 DEFAULT NULL,
    p_v1                  IN VARCHAR2 DEFAULT NULL,
    p_v2                  IN VARCHAR2 DEFAULT NULL,
    p_content_disposition IN VARCHAR2 DEFAULT NULL )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_item_name` | Name of valid application page item with type `FILE` that contains the source type of DB column. |
| `p_v1` | Value of primary key column 1. |
| `p_v2` | Value of primary key column 2. |
| `p_content_disposition` | Specify `INLINE` or `ATTACHMENT`, all other values ignored. |

---

## GET_BUILD_OPTION_STATUS Function Signature 1 (Deprecated)

Note:

This API is deprecated and will be removed in a future release.

Use GET_BUILD_OPTION_STATUS Function Signature 1 in APEX_APPLICATION_ADMIN instead.

Use this function to get the build option status of a specified application by providing the ID of the application build option.

Syntax

```sql
FUNCTION get_build_option_status(
    p_application_id   IN NUMBER,
    p_id               IN NUMBER )
    RETURN varchar2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_application_id` | The ID of the application that owns the build option under shared components. |
| `p_id` | The ID of the build option in the application. |

---

## GET_BUILD_OPTION_STATUS Function Signature 2 (Deprecated)

Note:

This API is deprecated and will be removed in a future release.

Use GET_BUILD_OPTION_STATUS Function Signature 2 in APEX_APPLICATION_ADMIN instead.

Use this function to get the build option status of a specified application by providing the name of the application build option.

Syntax

```sql
FUNCTION get_build_option_status (
    p_application_id     IN NUMBER
    p_build_option_name  IN VARCHAR2 )
    return VARCHAR2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_application_id` | The ID of the application that owns the build option under shared components. |
| `p_build_option_name` | The name of the build option in the application. |

---

## GET_CURRENT_USER_ID Function

This function returns the numeric user ID of the current user.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.GET_CURRENT_USER_ID
RETURN NUMBER;
```

Parameters

None.

---

## GET_DEFAULT_SCHEMA Function

This function returns the default schema name associated with the current user.

Syntax

```sql
APEX_UTIL.GET_DEFAULT_SCHEMA
RETURN VARCHAR2;
```

Parameters

None.

---

## GET_EDITION Function

This function returns the edition for the current page view.

Syntax

```sql
APEX_UTIL.GET_EDITION
RETURN VARCHAR2;
```

Parameters

None.

---

## GET_EMAIL Function

This function returns the email address associated with the named user.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.GET_EMAIL (
    p_username IN VARCHAR2 );
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | The user name in the account. |

---

## GET_FEEDBACK_FOLLOW_UP Function

Use this function to retrieve any remaining follow up associated with a specific feedback.

Syntax

```sql
APEX_UTIL.GET_FEEDBACK_FOLLOW_UP (
    p_feedback_id    IN NUMBER,
    p_row            IN NUMBER DEFAULT 1,
    p_template       IN VARCHAR2 DEFAULT '<br />#CREATED_ON# (#CREATED_BY#) #FOLLOW_UP#')
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_feedback_id` | The unique identifier of the feedback item. |
| `p_row` | Identifies which follow-up to retrieve and is ordered by `created_on_desc`. |
| `p_template` | The template to use to return the follow up. Given the `<br/>` in the default template, the function can be used in a loop to return all the follow up to a feedback. |

---

## GET_FILE Procedure

This procedure downloads files from the Oracle APEX file repository. If you invoke this procedure during page processing, ensure that no page branch is invoked under the same condition to avoid interference with the file retrieval. This means that branches with any of the following conditions should NOT be set to fire:

* Branches with a When Button Pressed attribute equal to the button that invokes the procedure.
* Branches with conditional logic defined that would succeed during page processing when the procedure is being invoked.
* As unconditional.

Syntax

```sql
APEX_UTIL.GET_FILE (
    p_file_id    IN VARCHAR2,
    p_inline     IN VARCHAR2 DEFAULT 'NO' );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_file_id` | ID in `APEX_APPLICATION_FILES` of the file to be downloaded. `APEX_APPLICATION_FILES` is a view on all files uploaded to your workspace. The following example demonstrates how to use `APEX_APPLICATION_FILES`:   ```sql DECLARE     l_file_id NUMBER; BEGIN     SELECT id         INTO l_file_id         FROM APEX_APPLICATION_FILES         WHERE filename = 'myxml';         --         APEX_UTIL.GET_FILE(             p_file_id   => l_file_id,              p_inline    => 'YES');   END; ``` |
| `p_inline` | Valid values include `YES` and `NO`. `YES` to display inline in a browser. `NO` to download as attachment. |

---

## GET_FILE_ID Function

This function obtains the primary key of a file in the Oracle APEX file repository.

Syntax

```sql
APEX_UTIL.GET_FILE_ID (
    p_name    IN VARCHAR2 )
RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | The NAME in `APEX_APPLICATION_FILES` of the file to be downloaded. `APEX_APPLICATION_FILES` is a view on all files uploaded to your workspace. |

---

## GET_FIRST_NAME Function

This function returns the `FIRST_NAME` field stored in the named user account record.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.GET_FIRST_NAME (
    p_username IN VARCHAR2 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | Identifies the user name in the account. |

---

## GET_GLOBAL_NOTIFICATION Function (Deprecated)

Note:

This API is deprecated and will be removed in a future release.

Use GET_GLOBAL_NOTIFICATION Function in APEX_APPLICATION_ADMIN instead.

This function gets the global notification message which is the message displayed in page `#GLOBAL_NOTIFICATION#` substitution string.

Syntax

```sql
APEX_UTIL.GET_GLOBAL_NOTIFICATION (
   p_application_id IN NUMBER ) RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The application ID. |

---

## GET_GROUPS_USER_BELONGS_TO Function

This function returns a comma then a space separated list of group names to which the named user is a member.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.GET_GROUPS_USER_BELONGS_TO (
   p_username IN VARCHAR2 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | Identifies the user name in the account. |

---

## GET_GROUP_ID Function

This function returns the numeric ID of a named group in the workspace.

Syntax

```sql
APEX_UTIL.GET_GROUP_ID (
    p_group_name IN VARCHAR2 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_group_name` | Identifies the name of a group in the workspace. |

---

## GET_GROUP_NAME Function

This function returns the name of a group identified by a numeric ID.

Syntax

```sql
APEX_UTIL.GET_GROUP_NAME (
    p_group_id IN NUMBER )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_group_id` | Identifies a numeric ID of a group in the workspace. |

---

## GET_HASH Function

This function computes a hash value for all given values. Use this function to implement lost update detection for data records.

Syntax

```sql
APEX_UTIL.GET_HASH (
    p_values IN apex_t_varchar2,
    p_salted IN BOOLEAN DEFAULT TRUE )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_values` | The input values. |
| `p_salted` | If TRUE (default), salt hash with internal session information. |

---

## GET_HIGH_CONTRAST_MODE_TOGGLE Function

This function returns a link to the current page that enables you to turn on or off, toggle, the mode. For example, if you are in standard mode, this function displays a link that when clicked switches high contrast mode on.

Syntax

```sql
APEX_UTIL.GET_HIGH_CONTRAST_MODE_TOGGLE (
    p_on_message  IN VARCHAR2 DEFAULT NULL,
    p_off_message IN VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_on_message` | Optional text used for the link to switch to high contrast mode, when you are in standard mode. If this parameter is not passed, the default 'Set High Contrast Mode On' text is returned in the link. |
| `p_off_message` | Optional text used for the link to switch to standard mode, when you are in high contrast mode. If this parameter is not passed, the default 'Set High Contrast Mode Off' text is returned in the link. |

---

## GET_LAST_NAME Function

This function returns the `LAST_NAME` field stored in the named user account record.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.GET_LAST_NAME (
    p_username IN VARCHAR2 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | The user name in the user account record. |

---

## GET_NUMERIC_SESSION_STATE Function

This function returns a numeric value for a numeric item. You can use this function in Oracle APEX applications wherever you can use PL/SQL or SQL. You can also use the shorthand function `NV` in place of `APEX_UTIL.GET_NUMERIC_SESSION_STATE`.

Tip:

For enhanced query performance, use FAST DUAL functionality in the following SQL code syntax:

```sql
(select apex_util.get_numeric_session_state('P1_ITEM') from dual)
```

Syntax

```sql
APEX_UTIL.GET_NUMERIC_SESSION_STATE (
    p_item  IN VARCHAR2 )
RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_item` | The case insensitive name of the item for which you want to have the session state fetched. |

---

## GET_PREFERENCE Function

This function retrieves the value of a previously saved preference for a given user.

Syntax

```sql
APEX_UTIL.GET_PREFERENCE (
    p_preference  IN    VARCHAR2 DEFAULT NULL,
    p_user        IN    VARCHAR2 DEFAULT V('USER') )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_preference` | Name of the preference to retrieve the value. |
| `p_user` | User for whom the preference is being retrieved. |

---

## GET_PRINT_DOCUMENT Function Signature 1

This function returns a document as BLOB using XML based report data and RTF or XSL-FO based report layout.

Syntax

```sql
APEX_UTIL.GET_PRINT_DOCUMENT (
    p_report_data         IN BLOB,
    p_report_layout       IN CLOB,
    p_report_layout_type  IN VARCHAR2 default 'xsl-fo',
    p_document_format     IN VARCHAR2 default 'pdf',
    p_print_server        IN VARCHAR2 default NULL )
RETURN BLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_report_data` | XML based report data. |
| `p_report_layout` | Report layout in XSL-FO or RTF format. |
| `p_report_layout_type` | Defines the report layout type, that is "xsl-fo" or "rtf". |
| `p_document_format` | Defines the document format, that is "pdf", "rtf", "xls", "htm", or "xml". |
| `p_print_server` | URL of the print server. If not specified, the print server is derived from preferences. |

---

## GET_PRINT_DOCUMENT Function Signature 2

This function returns a document as BLOB using pre-defined report query and pre-defined report layout.

Syntax

```sql
APEX_UTIL.GET_PRINT_DOCUMENT (
    p_application_id      IN NUMBER,
    p_report_query_name   IN VARCHAR2,
    p_report_layout_name  IN VARCHAR2 DEFAULT NULL,
    p_report_layout_type  IN VARCHAR2 DEFAULT 'xsl-fo',
    p_document_format     IN VARCHAR2 DEFAULT 'pdf',
    p_print_server        IN VARCHAR2 DEFAULT NULL )
RETURN BLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | Defines the application ID of the report query. |
| `p_report_query_name` | Name of the report query (stored under application's Shared Components). |
| `p_report_layout_name` | Name of the report layout (stored under application's Shared Components). |
| `p_report_layout_type` | Defines the report layout type, that is "xsl-fo" or "rtf". |
| `p_document_format` | Defines the document format, that is "pdf", "rtf", "xls", "htm", or "xml". |
| `p_print_server` | URL of the print server. If not specified, the print server is derived from preferences. |

---

## GET_PRINT_DOCUMENT Function Signature 3

This function returns a document as BLOB using a pre-defined report query and RTF or XSL-FO based report layout.

Syntax

```sql
APEX_UTIL.GET_PRINT_DOCUMENT (
    p_application_id      IN NUMBER,
    p_report_query_name   IN VARCHAR2,
    p_report_layout       IN CLOB,
    p_report_layout_type  IN VARCHAR2 DEFAULT 'xsl-fo',
    p_document_format     IN VARCHAR2 DEFAULT 'pdf',
    p_print_server        IN VARCHAR2 DEFAULT NULL )
RETURN BLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | Defines the application ID of the report query. |
| `p_report_query_name` | Name of the report query (stored under application's shared components). |
| `p_report_layout` | Defines the report layout in XSL-FO or RTF format. |
| `p_report_layout_type` | Defines the report layout type, that is "xsl-fo" or "rtf". |
| `p_document_format` | Defines the document format, that is "pdf", "rtf", "xls", "htm", or "xml". |
| `p_print_server` | URL of the print server. If not specified, the print server is derived from preferences. |

---

## GET_PRINT_DOCUMENT Function Signature 4

This function returns a document as `BLOB` using XML based report data and RTF or XSL-FO based report layout.

Syntax

```sql
APEX_UTIL.GET_PRINT_DOCUMENT (
    p_report_data         IN CLOB,
    p_report_layout       IN CLOB,
    p_report_layout_type  IN VARCHAR2 DEFAULT 'xsl-fo',
    p_document_format     IN VARCHAR2 DEFAULT 'pdf',
    p_print_server        IN VARCHAR2 DEFAULT NULL )
    RETURN BLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_report_data` | XML based report data, must be encoded in UTF-8. |
| `p_report_layout` | Report layout in XSL-FO or RTF format. |
| `p_report_layout_type` | Defines the report layout type, that is "xsl-fo" or "rtf". |
| `p_document_format` | Defines the document format, that is "pdf", "rtf", "xls", "htm", or "xml". |
| `p_print_server` | URL of the print server. If not specified, the print server is derived from preferences. |

---

## GET_SCREEN_READER_MODE_TOGGLE Function

This function returns a link to the current page to turn on or off, toggle, the mode. For example, if you are in standard mode, this function displays a link that when clicked switches screen reader mode on.

Syntax

```sql
APEX_UTIL.GET_SCREEN_READER_MODE_TOGGLE (
    p_on_message  IN VARCHAR2 DEFAULT NULL,
    p_off_message IN VARCHAR2 DEFAULT NULL )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_on_message` | Optional text used for the link to switch to screen reader mode, when you are in standard mode. If this parameter is not passed, the default 'Set Screen Reader Mode On' text is returned in the link. |
| `p_off_message` | Optional text used for the link to switch to standard mode, when you are in screen reader mode. If this parameter is not passed, the default 'Set Screen Reader Mode Off' text is returned in the link. |

---

## GET_SESSION_LANG Function

This function returns the language setting for the current user in the current Oracle APEX session.

Syntax

```sql
APEX_UTIL.GET_SESSION_LANG
RETURN VARCHAR2;
```

Parameters

None.

---

## GET_SESSION_STATE Function

This function returns the value for an item. You can use this function in your Oracle APEX applications wherever you can use PL/SQL or SQL. You can also use the shorthand function `V` in place of `APEX_UTIL.GET_SESSION_STATE`.

Tip:

For enhanced query performance, use FAST DUAL functionality in the following SQL code syntax:

```sql
(select apex_util.get_session_state('P1_ITEM') from dual)
```

Syntax

```sql
APEX_UTIL.GET_SESSION_STATE (
    p_item  IN VARCHAR2 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_item` | The case insensitive name of the item for which you want to have the session state fetched. |

---

## GET_SESSION_TERRITORY Function

This function returns the territory setting for the current user in the current Oracle APEX session.

Syntax

```sql
APEX_UTIL.GET_SESSION_TERRITORY
RETURN VARCHAR2;
```

Parameters

None.

---

## GET_SESSION_TIME_ZONE Function

This function returns the time zone for the current user in the current Oracle APEX session. This value is null if the time zone is not explicitly set by using `APEX_UTIL.SET_SESSION_TIME_ZONE` or if an application's automatic time zone attribute is enabled.

Syntax

```sql
APEX_UTIL.GET_SESSION_TIME_ZONE
RETURN VARCHAR2;
```

Parameters

None.

---

## GET_SINCE Function Signature 1

This function returns the relative date in words (for example, 2 days from now, 30 minutes ago). It also accepts a second optional `p_short` parameter and returns "in 2d" or "30m" and so forth. This function is equivalent to using the format masks `SINCE` and `SINCE_SHORT` available within Oracle APEX and is useful within SQL queries or PL/SQL routines.

Syntax

```sql
APEX_UTIL.GET_SINCE (
   p_date  DATE )
   p_short IN [ BOOLEAN DEFAULT FALSE | VARCHAR2 DEFAULT 'N' ] )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_date` | The date you want formatted. |
| `p_short` | Boolean or Y/N to indicate whether to return a short version of relative date. |

---

## GET_SINCE Function Signature 2

This function returns the relative date in words (for example, 2 days from now, 30 minutes ago). It also accepts a second optional `p_short` parameter and returns "in 2d" or "30m" and so forth. This function is equivalent to using the format masks `SINCE` and `SINCE_SHORT` available within Oracle APEX and is useful within SQL queries or PL/SQL routines.

Syntax

```sql
APEX_UTIL.GET_SINCE (
   p_value in [ timestamp | timestamp with time zone | timestamp with local time zone ],
   p_short in [ boolean default false | varchar2 default 'N' ] )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | The `TIMESTAMP`, `TIMESTAMP WITH TIME ZONE`, `TIMESTAMP WITH LOCAL TIME ZONE` you want to format. |
| `p_short` | Boolean or Y/N to indicate whether to return a short version of relative date. |

---

## GET_SUPPORTING_OBJECT_SCRIPT Function

This function gets supporting object scripts defined in an application.

Note:

The workspace ID must be set before the call.

Syntax

```sql
APEX_UTIL.GET_SUPPORTING_OBJECT_SCRIPT (
    p_application_id  IN NUMBER,
    p_script_type     IN VARCHAR2 )
RETURN CLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The application ID to get supporting objects from. |
| `p_script_type` | The supporting objects script type. Valid values are `apex_util.c_install_script`, `apex_util.c_upgrade_script`, `apex_util.c_deinstall_script`. |

---

## GET_SUPPORTING_OBJECT_SCRIPT Procedure

This procedure gets supporting object scripts and outputs to `sys.dbms_output` buffer or download as a file.

Note:

The workspace ID must be set before the call.

Syntax

```sql
APEX_UTIL.GET_SUPPORTING_OBJECT_SCRIPT (
    p_application_id  IN NUMBER,
    p_script_type     IN VARCHAR2,
    p_output_type     IN VARCHAR2 DEFAULT c_output_as_dbms_output );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The application ID to get supporting objects from. |
| `p_script_type` | The supporting objects script type. Valid values are `apex_util.c_install_script`, `apex_util.c_upgrade_script`, `apex_util.c_deinstall_script`. |
| `p_output_type` | The script can be output to `sys.dbms_output` buffer or download as a file. Valid values are `apex_util.c_output_as_dbms_output`, `apex_util.c_output_as_file`. The default is `c_output_as_dbms_output`. |

---

## GET_USER_ID Function

This function returns the numeric ID of a named user in the workspace.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.GET_USER_ID (
    p_username   IN VARCHAR2 )
RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | Identifies the name of a user in the workspace. |

---

## GET_USER_ROLES Function

This function returns the `DEVELOPER_ROLE` field stored in the named user account record.

Syntax

```sql
APEX_UTIL.GET_USER_ROLES (
    p_username  IN  VARCHAR2 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | Identifies a user name in the account. |

---

## GET_USERNAME Function

This function returns the user name of a user account identified by a numeric ID.

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with Oracle APEX Accounts authentication.

Syntax

```sql
APEX_UTIL.GET_USERNAME (
    p_userid    IN NUMBER )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_userid` | Identifies the numeric ID of a user account in the workspace. |

---

## HOST_URL Function

This function returns the URL to the Oracle APEX instance, depending on the option passed.

Syntax

```sql
APEX_UTIL.HOST_URL (
    p_option    IN VARCHAR2 DEFAULT NULL )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_option` | Specifies the parts of the URL to include.  Possible values for `p_option` include:   * `NULL` - Return URL up to port number. For example:  `http://example.com:7778` * `SCRIPT` - Return URL to include script name. For example:  For example (Friendly URL enabled):  `https://example.com:7778/pls/apex/r/{workspace}/{application}`  For example (Friendly URL disabled)  `https://example.com:7778/pls/apex/` * `APEX_PATH` - Return URL to include the APEX path. For example:  `https://example.com:7778/pls/apex/` * `IMGPRE` - Return URL to include image prefix. For example:  `https://example.com:7778/i/` |

---

## HTML_PCT_GRAPH_MASK Function

Use this function to scale a graph. This function can also be used by classic and interactive reports with format mask of GRAPH. This generates a `<div>` tag with inline styles.

Syntax

```sql
APEX_UTIL.HTML_PCT_GRAPH_MASK (
    p_number          IN NUMBER    DEFAULT NULL,
    p_size            IN NUMBER    DEFAULT 100,
    p_background      IN VARCHAR2  DEFAULT NULL,
    p_bar_background  IN VARCHAR2  DEFAULT NULL,
    p_format          IN VARCHAR2  DEFAULT NULL,
    p_aria_labelledby IN VARCHAR2  DEFAULT NULL,
    p_aria_label      IN VARCHAR2  DEFAUL  NULL )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_number` | Number between 0 and 100. |
| `p_size` | Width of graph in pixels. |
| `p_background` | Six character hexadecimal background color of chart bar (not bar color). |
| `p_bar_background` | Six character hexadecimal background color of chart bar (bar color). |
| `p_format` | If this parameter is supplied, `p_size`, `p_background` and `p_bar_background` are ignored.  This parameter uses the following format:  `PCT_GRAPH`:<`BACKGROUND`>:<`FOREGROUND`>:<`CHART_WIDTH`>  position 1: PCT_GRAPH format mask indicator  position 2: Background color in hexadecimal, 6 characters (optional)  position 3: Foreground "bar" color in hexadecimal, 6 characters (optional)  position 4: Chart width in pixels. Numeric and defaults to 100.  `p_number` is automatically scaled so that 50 is half of `chart_width` (optional). |
| `p_aria_labelledby` | Space-separated list of one or more ID values referencing the elements that label the percent graph. |
| `p_aria_label` | Value that labels the percent graph. |

---

## INCREMENT_CALENDAR Procedure (Deprecated)

Note:

This API is deprecated and will be
removed in a future release.

Use this procedure to navigate to the next set of days in the calendar. Depending on what the calendar view is, this procedure navigates to the next month, week or day. If it is a Custom Calendar the total number of days between the start date and end date are navigated.

Syntax

```sql
APEX_UTIL.INCREMENT_CALENDAR;
```

Parameters

None.

---

## IR_CLEAR Procedure (Deprecated)

Note:

The use of this procedure is not recommended. This procedure has been replaced by the procedure in APEX_IR.

This procedure clears report settings. Only use this procedure in a page submit process.

Syntax

```sql
APEX_UTIL.IR_CLEAR (
    p_page_id       IN NUMBER,
    p_report_alias  IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_page_id` | Page of the current Oracle APEX application that contains an interactive report. |
| `p_report_alias` | Identifies the saved report alias within the current application page.  To clear a Primary report, set `p_report_alias` to `PRIMARY` or leave as NULL.  To clear a saved report, `p_report_alias` must be the name of the saved report. For example, to clear report `1234`, set `p_report_alias` to `1234`. |

---

## IR_DELETE_REPORT Procedure (Deprecated)

Note:

Use of this procedure is not recommended. This procedure has been replaced by the procedure in APEX_IR.

This procedure deletes saved interactive reports. It deletes all saved reports except the Primary Default report.

Syntax

```sql
APEX_UTIL.IR_DELETE_REPORT (
    p_report_id     IN NUMBER );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_report_id` | Report ID to delete within the current Oracle APEX application. |

---

## IR_DELETE_SUBSCRIPTION Procedure (Deprecated)

Note:

The use of this procedure is not recommended. This procedure has been replaced by the procedure in APEX_IR.

This procedure deletes Interactive subscriptions.

Syntax

```sql
APEX_UTIL.IR_DELETE_SUBSCRIPTION(
    p_subscription_id IN NUMBER);
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_subscription_id` | Subscription ID to delete within the current workspace. |

---

## IR_FILTER Procedure (Deprecated)

Note:

This procedure is not recommended. This procedure has been replaced by the procedure in APEX_IR.

This procedure creates a filter on an interactive report. Only use this procedure in a page submit process.

Syntax

```sql
APEX_UTIL.IR_FILTER (
    p_page_id       IN NUMBER,
    p_report_column IN VARCHAR2,
    p_operator_abbr IN VARCHAR2 DEFAULT NULL,
    p_filter_value  IN VARCHAR2,
    p_report_alias  IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_page_id` | Page of the current Oracle APEX application that contains an interactive report. |
| `p_report_column` | Name of the report SQL column, or column alias, to be filtered. |
| `p_operator_abbr` | Filter type. Valid values are as follows:   * `EQ` = Equals * `NEQ` = Not Equals * `LT` = Less than * `LTE` = Less then or equal to * `GT` = Greater Than * `GTE` = Greater than or equal to * `LIKE` = SQL Like operator * `N` = Null * `NN` = Not Null * `C` = Contains * `NC` = Not Contains * `IN` = SQL In Operator * `NIN` = SQL Not In Operator |
| `p_filter_value` | Filter value. This value is not used for `N` and `NN`. |
| `p_report_alias` | Identifies the saved report alias within the current application page. To create a filter on a Primary report, `p_report_alias` must be `PRIMARY` or leave as NULL. To create a filter on a saved report, `p_report_alias` must be the name of the saved report. For example, to create a filter on report `1234`, `p_report_alias` must be `1234`. |

---

## IR_RESET Procedure (Deprecated)

Note:

The use of this procedure is not recommended. This procedure has been replaced by the procedure in APEX_IR.

This procedure resets report settings back to the default report settings. Resetting a report removes any customizations you have made.

Note:

This procedure should be used only in a page submit process.

Syntax

```sql
APEX_UTIL.IR_RESET(
    p_page_id IN NUMBER,
    p_report_alias IN VARCHAR2 DEFAULT NULL);
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_page_id` | Page of the current Oracle APEX application that contains an interactive report. |
| `p_report_alias` | Identifies the saved report alias within the current application page. To reset a Primary report, `p_report_alias` must be 'PRIMARY' or leave as NULL. To reset a saved report, `p_report_alias` must be the name of the saved report. For example, to reset report '1234', `p_report_alias` must be '1234'. |

---

## IS_HIGH_CONTRAST_SESSION Function

This function returns a boolean TRUE if the session is in high contrast mode and returns a boolean FALSE if not in high contrast mode.

Syntax

```sql
APEX_UTIL.IS_HIGH_CONTRAST_SESSION
RETURN BOOLEAN;
```

Parameters

None.

---

## IS_HIGH_CONTRAST_SESSION_YN Function

This function returns `Y` if the session is in high contrast mode and `N` if not in high contrast mode.

Syntax

```sql
APEX_UTIL.IS_HIGH_CONTRAST_SESSION_YN
RETURN VARCHAR2;
```

Parameters

None.

---

## IS_LOGIN_PASSWORD_VALID Function

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with APEX Accounts authentication.

This function returns a Boolean result based on the validity of the password for a named user account in the current workspace. This function returns TRUE if the password matches and it returns FALSE if the password does not match.

Syntax

```sql
APEX_UTIL.IS_LOGIN_PASSWORD_VALID (
    p_username IN VARCHAR2 DEFAULT NULL,
    p_password IN VARCHAR2 DEFAULT NULL )
RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | User name in account. |
| `p_password` | Password to be compared with password stored in the account. |

Returns

* `true`: The user credentials are valid.
* `false`: The user credentials are invalid.
* `null`: Credentials checking was delayed because of too many wrong combinations.

---

## IS_SCREEN_READER_SESSION Function

This function returns a boolean TRUE if the session is in screen reader mode and returns a boolean FALSE if not in screen reader mode.

Syntax

```sql
APEX_UTIL.IS_SCREEN_READER_SESSION
RETURN BOOLEAN;
```

Parameters

None

---

## IS_SCREEN_READER_SESSION_YN Function

This function returns 'Y' if the session is in screen reader mode and 'N' if not in screen reader mode.

Syntax

```sql
APEX_UTIL.IS_SCREEN_READER_SESSION_YN
RETURN VARCHAR2;
```

Parameters

None

---

## IS_USERNAME_UNIQUE Function

Note:

This function operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with APEX Accounts authentication.

This function returns a Boolean result based on whether the named user account is unique in the workspace.

Syntax

```sql
APEX_UTIL.IS_USERNAME_UNIQUE (
    p_username IN VARCHAR2 )
RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | Identifies the user name to be tested. |

---

## KEYVAL_NUM Function

This function gets the value of the package variable (`apex_utilities.g_val_num`) set by `APEX_UTIL.SAVEKEY_NUM`.

Syntax

```sql
APEX_UTIL.KEYVAL_NUM
RETURN NUMBER;
```

Parameters

None

---

## KEYVAL_VC2 Function

This function gets the value of the package variable (`apex_utilities.g_val_vc2`) set by `APEX_UTIL.SAVEKEY_VC2`.

Syntax

```sql
APEX_UTIL.KEYVAL_VC2;
```

Parameters

None.

---

## LOCK_ACCOUNT Procedure

This procedure sets a user account status to locked. Must be run by an authenticated workspace administrator in the context of a page request.

Syntax

```sql
APEX_UTIL.LOCK_ACCOUNT (
     p_user_name IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## PASSWORD_FIRST_USE_OCCURRED Function

This function returns `TRUE` if the account's password has changed since the account was created, an Oracle APEX administrator performs a password reset operation that results in a new password being emailed to the account holder, or a user has initiated password reset operation.

This function returns `FALSE` if the account's password has not been changed since either of the events just described.

This function may be run in a page request context by any authenticated user.

Syntax

```sql
APEX_UTIL.PASSWORD_FIRST_USE_OCCURRED (
    p_user_name     IN VARCHAR2 )
RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## PREPARE_URL Function

Note:

Oracle recommends using `APEX_PAGE.GET_URL` instead of `PREPARE_URL` for improved readability.

See GET_URL Function.

The PREPARE_URL function serves two purposes:

1. To return an APEX navigation URL with the Session State Protection checksum argument (&cs=) if one is required. For security, the URL will not contain a checksum if the specified application is located in a different workspace.
2. To return an APEX navigation URL with the session ID component replaced with zero (0) if the zero session ID feature is in use and other criteria are met.

Note:

The `PREPARE_URL` function returns the APEX navigation URL with `&cs=<large hex value>` appended. If you use this returned value (such as in JavaScript), you may need to escape the ampersand in the URL to conform with syntax rules of the particular context.

Syntax

```sql
APEX_UTIL.PREPARE_URL (
    p_url                    IN VARCHAR2,
    p_url_charset            IN VARCHAR2 DEFAULT NULL,
    p_checksum_type          IN VARCHAR2 DEFAULT NULL,
    p_triggering_element     IN VARCHAR2 DEFAULT 'this',
    p_plain_url              IN BOOLEAN  DEFAULT FALSE,
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_url` | An APEX navigation URL with all substitutions resolved. |
| `p_url_charset` | The character set name (for example, `UTF-8`) to use when escaping special characters contained within argument values. |
| `p_checksum_type` | Null or any of the following values:   * `PUBLIC_BOOKMARK` or `1` - Use this when generating links to be used by any user. For example, use this value when generating an email which includes links to an application. * `PRIVATE_BOOKMARK` or `2` - Use this when generating a link to be used outside of the current session. This option can only be used by the same currently authenticated user. * `SESSION` or `3` - Use this when generating links to an application. This option can only be used within the current session. |
| `p_triggering_element` | A jQuery selector (for example, `#my_button` , where `my_button` is the static ID for a button element), to identify which element to use to trigger the dialog. This is required for Modal Dialog support. |
| `p_plain_url` | If the page you are calling `APEX_UTIL.PREPARE_URL` from is a modal dialog, specify `p_plain_url` to omit the unnecessary dialog code in the generated link. By default, if this function is called from a modal dialog, extra code to close the modal dialog is included in the generated URL. |

---

## PRN Procedure

This procedure prints a given CLOB to the HTP buffer.

Syntax

```sql
APEX_UTIL.PRN (
    p_clob   IN CLOB,
    p_escape IN BOOLEAN DEFAULT TRUE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_clob` | The CLOB. |
| `p_escape` | If `TRUE` (default), escape special characters, using apex_escape.html. |

---

## PUBLIC_CHECK_AUTHORIZATION Function (Deprecated)

Note:

This API is deprecated and will be
removed in a future release.

Use the IS_AUTHORIZED Function instead of this deprecated function.

Given the name of a authorization scheme, this function determines if the current user passes the security check.

Syntax

```sql
APEX_UTIL.PUBLIC_CHECK_AUTHORIZATION (
    p_security_scheme    IN    VARCHAR2 )
RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_security_scheme` | The name of the authorization scheme that determines if the user passes the security check. |

---

## PURGE_REGIONS_BY_APP Procedure

Deletes all cached regions for an application.

Syntax

```sql
APEX_UTIL.PURGE_REGIONS_BY_APP (
    p_application IN NUMBER );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application` | The identification number (ID) of the application. |

---

## PURGE_REGIONS_BY_NAME Procedure

Deletes all cached values for a region identified by the application ID, page number and region name.

Syntax

```sql
APEX_UTIL.PURGE_REGIONS_BY_NAME (
     p_application IN NUMBER,
     p_page        IN NUMBER,
     p_region_name IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application` | The identification number (ID) of the application. |
| `p_page` | The number of the page containing the region to be deleted. |
| `p_region_name` | The region name to be deleted. |

---

## PURGE_REGIONS_BY_PAGE Procedure

Deletes all cached regions by application and page.

Syntax

```sql
APEX_UTIL.PURGE_REGIONS_BY_PAGE (
     p_application IN NUMBER,
     p_page        IN NUMBER );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application` | The identification number (ID) of the application. |
| `p_page` | The identification number of page containing the region. |

---

## REDIRECT_URL Procedure

This procedure calls `owa_util.redirect_url` to tell the browser to redirect to a new URL. Afterwards, it automatically calls `apex_application.stop_apex_engine` to cancel further processing of the Oracle APEX application.

Syntax

```sql
APEX_UTIL.REDIRECT_URL (
    p_url               IN VARCHAR2,
    p_reset_htp_buffer  IN BOOLEAN  DEFAULT TRUE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_url` | The URL the browser requests. |
| `p_reset_htp_buffer` | Set to `TRUE` to reset the HTP buffer to make sure the browser understands the redirect to the new URL and is not confused by data that is already written to the HTP buffer. Set to `FALSE` if the application has its own cookie to use in the response. |

---

## REMOVE_PREFERENCE Procedure

This procedure removes the preference for the supplied user.

Syntax

```sql
APEX_UTIL.REMOVE_PREFERENCE(
    p_preference    IN    VARCHAR2 DEFAULT NULL,
    p_user          IN    VARCHAR2 DEFAULT V('USER') );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_preference` | Name of the preference to remove. |
| `p_user` | User for whom the preference is defined. |

---

## REMOVE_SORT_PREFERENCES Procedure

This procedure removes the user's column heading sorting preference value.

Syntax

```sql
APEX_UTIL.REMOVE_SORT_PREFERENCES (
    p_user  IN   VARCHAR2 DEFAULT V('USER') );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user` | Identifies the user for whom sorting preferences are removed. |

---

## REMOVE_USER Procedure Signature 1

This procedure removes the user account identified by the primary key. To execute this procedure, the current user must have administrative privilege in the workspace.

Syntax

```sql
APEX_UTIL.REMOVE_USER (
    p_user_id   IN NUMBER );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_id` | The numeric primary key of the user account record. |

---

## REMOVE_USER Procedure Signature 2

This procedure removes the user account identified by the user name. To execute this procedure, the current user must have administrative privilege in the workspace.

Syntax

```sql
APEX_UTIL.REMOVE_USER (
    p_user_name IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## REPLY_TO_FEEDBACK Procedure

This procedure enables you to submit a reply to a feedback.

Syntax

```sql
APEX_UTIL.REPLY_TO_FEEDBACK (
    p_feedback_id        IN NUMBER,
    p_type               IN NUMBER   DEFAULT NULL,
    p_status             IN NUMBER   DEFAULT NULL,
    p_tags               IN VARCHAR2 DEFAULT NULL,
    p_developer_comment  IN VARCHAR2 DEFAULT NULL,
    p_public_response    IN VARCHAR2 DEFAULT NULL,
    p_followup           IN VARCHAR2 DEFAULT NULL )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_feedback_id` | The ID of feedback. |
| `p_type` | The type of feedback (1 is General Comment, 2 is Enhancement Request, 3 is Bug). |
| `p_status` | The status of the feedback (0 is No Action, 1 is Acknowledged, 3 is Open and 4 is Closed). |
| `p_tags` | Used to categorize feedback, only to be displayed to developers (not in the current feature implementation). |
| `p_developer_comment` | Comments not displayed to the users but could be displayed to developers (not in the current feature implementation). |
| `p_public_response` | Text that will be displayed to the users. |
| `p_followup` | The text of the follow-up. When the Feedback feature is added to an application, it only uses `p_public_response`. It does not support passing data to `p_followup`. |

---

## RESET_AUTHORIZATIONS Procedure (Deprecated)

Note:

Use the RESET_CACHE Procedure instead of this deprecated procedure.

To increase performance, Oracle APEX caches the results of authorization schemes after they have been evaluated. You can use this procedure to undo caching, requiring each authorization scheme be revalidated when it is next encountered during page show or accept processing. You can use this procedure if you want users to have the ability to change their responsibilities (their authorization profile) within your application.

Syntax

```sql
APEX_UTIL.RESET_AUTHORIZATIONS;
```

Parameters

None.

---

## RESET_PASSWORD Procedure

This procedure changes the password of `p_user_name` in the current workspace to `p_new_password`. If `p_change_password_on_first_use` is TRUE, then the user has to change the password on the next login.

Syntax

```sql
APEX_UTIL.RESET_PASSWORD (
    p_user_name                     IN VARCHAR2 DEFAULT apex_application.g_user,
    p_old_password                  IN VARCHAR2 DEFAULT NULL,
    p_new_password                  IN VARCHAR2,
    p_change_password_on_first_use  IN BOOLEAN  DEFAULT TRUE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user whose password should be changed. The default is the currently logged in Oracle APEX user name. |
| `p_old_password` | The current password of the user. The call succeeds if the given value matches the current password or it is NULL and the owner of the calling PL/SQL code has APEX_ADMINISTRATOR_ROLE. If the value is not the user's password, an error occurs. |
| `p_new_password` | The new password. |
| `p_change_password_on_first_use` | If `TRUE` (default), the user must change the password on the next login. |

Errors Raised

| Error | Description |
| --- | --- |
| INVALID_CREDENTIALS | Occurs if `p_user_name` does not match `p_old_password`. |
| `APEX.AUTHENTICATION.LOGIN_THROTTLE.COUNTER` | Indicates authentication prevented by login throttle. |
| `internal error` | Occurs if `p_old_password` is NULL and caller does not have `APEX_ADMINISTRATOR_ROLE`. |
| `internal error` | Indicates caller is not a valid workspace schema. |

---

## RESET_PW Procedure

This procedure resets the password for a named user and emails it in a message to the email address located for the named account in the current workspace. To execute this procedure, the current user must have administrative privilege in the workspace.

Syntax

```sql
APEX_UTIL.RESET_PW (
    p_user IN VARCHAR2,
    p_msg  IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user` | The user name of the user account. |
| `p_msg` | Message text to be mailed to a user. |

---

## SAVEKEY_NUM Function

This function sets a package variable (`apex_utilities.g_val_num`) so that it can be retrieved using the function `KEYVAL_NUM`.

Syntax

```sql
APEX_UTIL.SAVEKEY_NUM (
    p_val IN NUMBER )
RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_val` | The numeric value to be saved. |

---

## SAVEKEY_VC2 Function

This function sets a package variable (`apex_utilities.g_val_vc2`) so that it can be retrieved using the function `KEYVAL_VC2`.

Syntax

```sql
APEX_UTIL.SAVEKEY_VC2 (
    p_val IN VARCHAR2 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_val` | The is the VARCHAR2 value to be saved. |

---

## SET_APP_BUILD_STATUS Procedure (Deprecated)

Note:

This API is deprecated and will be removed in a future release.

Use SET_BUILD_STATUS Procedure in APEX_APPLICATION_ADMIN instead.

This procedure sets the build status of the specified application.

Syntax

```sql
APEX_UTIL.SET_APP_BUILD_STATUS (
    p_application_id  IN NUMBER,
    p_build_status    IN VARCHAR2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The ID of the application. |
| `p_build_status` | The new build status of the application.  Values include:   * `RUN_ONLY` - The application can be run but cannot be edited by developers. * `RUN_AND_BUILD` - The application can be run and can also be edited by developers. |

---

## SET_APPLICATION_STATUS Procedure (Deprecated)

Note:

This API is deprecated and will be removed in a future release.

Use SET_APPLICATION_STATUS Procedure in APEX_APPLICATION_ADMIN instead.

This procedure changes the status of the application.

Syntax

```sql
APEX_UTIL.SET_APPLICATION_STATUS (
   p_application_id        IN NUMBER,
   p_application_status    IN VARCHAR2,
   p_unavailable_value     IN VARCHAR2,
   p_restricted_user_list  IN VARCHAR2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The Application ID. |
| `p_application_status` | New application status.  Values include:   * `AVAILABLE` - Application is available with no restrictions. * `AVAILABLE_W_EDIT_LINK` - Application is available with no restrictions. Developer Toolbar shown to developers. * `DEVELOPERS_ONLY` - Application only available to developers. * `RESTRICTED_ACCESS` - Application only available to users in `p_restricted_user_list`. * `UNAVAILABLE` - Application unavailable. Message shown in `p_unavailable_value`. * `UNAVAILABLE_PLSQL` - Application unavailable. Message shown from PL/SQL block in `p_unavailable_value`. * `UNAVAILABLE_URL` - Application unavailable. Redirected to URL provided in `p_unavailable_value`. |
| `p_unavailable_value` | Value used when application is unavailable.  This value has different semantics dependent upon value for `p_application_status`. |
| `p_restricted_user_list` | Comma separated list of users permitted to access application, when `p_application_status = RESTRICTED_ACCESS`. |

---

## SET_ATTRIBUTE Procedure

This procedure sets the value of one of the attribute values (1 through 10) of a user in the Oracle APEX accounts table.

Syntax

```sql
APEX_UTIL.SET_ATTRIBUTE (
    p_userid           IN NUMBER,
    p_attribute_number IN NUMBER,
    p_attribute_value  IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_userid` | The numeric ID of the user account. |
| `p_attribute_number` | Attribute number in the user record (1 through 10). |
| `p_attribute_value` | Value of the attribute located by `p_attribute_number` to be set in the user record. |

---

## SET_AUTHENTICATION_RESULT Procedure

This procedure can be called from an application's custom authentication function (that is, credentials verification function). The status passed to this procedure is logged in the Login Access Log.

Syntax

```sql
APEX_UTIL.SET_AUTHENTICATION_RESULT (
    p_code IN NUMBER );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_code` | Any numeric value the developer chooses. After this value is set in the session using this procedure, it can be retrieved using the `APEX_UTIL.GET_AUTHENTICATION_RESULT` function. |

---

## SET_BUILD_OPTION_STATUS Procedure (Deprecated)

Note:

This API is deprecated and will be removed in a future release.

Use SET_BUILD_OPTION_STATUS Procedure in APEX_APPLICATION_ADMIN instead.

Use this procedure to change the build option status of a specified application.

Note:

The build option status will be overwritten when the application is upgraded to a new version. To keep the status set via the API, it is necessary to set the build option attribute On Upgrade Keep Status to Yes.

Syntax

```sql
APEX_UTIL.SET_BUILD_OPTION_STATUS (
    p_application_id IN NUMBER,
    p_id             IN NUMBER,
    p_build_status   IN VARCHAR2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The ID of the application that owns the build option under shared components. |
| `p_id` | The ID of the build option in the application. |
| `p_build`_status | The new status of the build option. Possible values are `INCLUDE`, `EXCLUDE` both upper case. |

---

## SET_CURRENT_THEME_STYLE Procedure (Deprecated)

Note:

This API is deprecated and will be
removed in a future release.

This procedure sets the user interface theme style for an application. For example, if there are more than one theme styles available for the current theme, you can use this procedure to change the application theme style.

Syntax

```sql
APEX_UTIL.SET_CURRENT_THEME_STYLE(
    p_theme_number   IN NUMBER,
    p_theme_style_id IN NUMBER );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_theme_number` | The current theme number of the application. This can be retrieved from `APEX_APPLICATION_THEMES` view. |
| `p_theme_style_id` | The numeric ID of theme style. You can get available theme styles for an application from `APEX_APPLICATION_THEME_STYLES` view. |

---

## SET_CUSTOM_AUTH_STATUS Procedure

This procedure can be called from an application's custom authentication function (that is, credentials verification function). The status passed to this procedure is logged in the Login Access Log.

Syntax

```sql
APEX_UTIL.SET_CUSTOM_AUTH_STATUS (
    p_status  IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_status` | Any text the developer chooses to denote the result of the authentication attempt (up to 4000 characters). |

---

## SET_EDITION Procedure

This procedure sets the name of the edition to be used in all application SQL parsed in the current page view or page submission.

Syntax

```sql
APEX_UTIL.SET_EDITION (
    p_edition IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_edition` | Edition name. |

---

## SET_EMAIL Procedure

This procedure updates a user account with a new email address. To execute this procedure, the current user must have administrative privileges in the workspace.

Syntax

```sql
APEX_UTIL.SET_EMAIL (
    p_userid IN NUMBER,
    p_email  IN VARCHAR2 );
```

Parameters

SET_EMAIL Parameters

| Parameter | Description |
| --- | --- |
| `p_userid` | The numeric ID of the user account. |
| `p_email` | The email address to be saved in user account. |

---

## SET_FIRST_NAME Procedure

Note:

This procedure operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with APEX Accounts authentication.

This procedure updates a user account with a new `FIRST_NAME` value. To execute this procedure, the current user must have administrative privileges in the workspace.

Syntax

```sql
APEX_UTIL.SET_FIRST_NAME (
    p_userid      IN NUMBER,
    p_first_name  IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_userid` | The numeric ID of the user account. |
| `p_first_name` | `FIRST_NAME` value to be saved in user account. |

---

## SET_GLOBAL_NOTIFICATION Procedure (Deprecated)

Note:

This API is deprecated and will be removed in a future release.

Use SET_GLOBAL_NOTIFICATION Procedure in APEX_APPLICATION_ADMIN instead.

This procedure is used to set the global notification message which is the message displayed in page `#GLOBAL_NOTIFICATION#` substitution string.

Syntax

```sql
APEX_UTIL.SET_GLOBAL_NOTIFICATION (
   p_application_id              IN NUMBER,
   p_global_notification_message IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The Application ID. |
| `p_global_notification_message` | Text string to be used for the global notification message. |

---

## SET_GROUP_GROUP_GRANTS Procedure

This procedure modifies the group grants for a given group.

Syntax

```sql
APEX_UTIL.SET_GROUP_GROUP_GRANTS (
    p_group_name          IN VARCHAR2,
    p_granted_group_names IN apex_t_varchar2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_group_name` | The target group name. |
| `p_granted_group_names` | The names of groups to grant to `p_group_name`. |

---

## SET_GROUP_USER_GRANTS Procedure

This procedure modifies the group grants for a given user.

Syntax

```sql
APEX_UTIL.SET_GROUP_USER_GRANTS (
    p_user_name IN VARCHAR2,
    p_granted_group_names IN apex_t_varchar2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The target user name. |
| `p_granted_group_names` | The names of groups to grant to `p_user_name`. |

---

## SET_LAST_NAME Procedure

Note:

This procedure operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with APEX Accounts authentication.

This procedure updates a user account with a new `LAST_NAME` value. To execute this procedure, the current user must have administrative privileges in the workspace.

Syntax

```sql
APEX_UTIL.SET_LAST_NAME (
    p_userid      IN NUMBER,
    p_last_name   IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_userid` | The numeric ID of the user account. |
| `p_last_name` | `LAST_NAME` value to be saved in the user account. |

---

## SET_PARSING_SCHEMA_FOR _REQUEST Procedure

This procedure changes the parsing user for the current page view to another workspace schema. You can call this procedure only from within the application's Initialization PL/SQL Code.

Syntax

```sql
APEX_UTIL.SET_PARSING_SCHEMA_FOR_REQUEST (
    p_schema IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_schema` | The new parsing schema. |

Raises

`PROGRAM_ERROR` when not called from Initialization PL/SQL Code. `WWV_FLOW.NO_PRIV_ON_SCHEMA` if `p_schema` is not a valid workspace schema.

---

## SET_PREFERENCE Procedure

This procedure sets a preference that persists beyond the user's current session.

Syntax

```sql
APEX_UTIL.SET_PREFERENCE (
    p_preference   IN    VARCHAR2 DEFAULT NULL,
    p_value        IN    VARCHAR2 DEFAULT NULL,
    p_user         IN    VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_preference` | Name of the preference (case-sensitive). |
| `p_value` | Value of the preference. |
| `p_user` | User for whom the preference is being set. |

---

## SET_SECURITY_GROUP_ID Procedure

Use this procedure with `apex_util.find_security_group_id` to ease the use of the mail package in batch mode. This procedure is especially useful when a schema is associated with more than one workspace. For example, you might want to create a procedure that is run by a nightly job to email all outstanding tasks.

Syntax

```sql
APEX_UTIL.SET_SECURITY_GROUP_ID (
    p_security_group_id  IN NUMBER);
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_security_group_id` | This is the security group id of the workspace you are working in. |

---

## SET_SESSION_HIGH_CONTRAST_OFF Procedure

This procedure switches off high contrast mode for the current session.

Syntax

```sql
APEX_UTIL.SET_SESSION_HIGH_CONTRAST_OFF;
```

Parameters

None.

---

## SET_SESSION_HIGH_CONTRAST_ON Procedure

This procedure switches on high contrast mode for the current session.

Syntax

```sql
APEX_UTIL.SET_SESSION_HIGH_CONTRAST_ON;
```

Parameters

None.

---

## SET_SESSION_LANG Procedure

This procedure sets the language for the current user in the current Oracle APEX session. The language must be a valid IANA language name.

Syntax

```sql
APEX_UTIL.SET_SESSION_LANG (
    p_lang IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_lang` | This is an IANA language code. Examples include en, de, de-at, zh-cn, and pt-br. |

---

## SET_SESSION_LIFETIME_SECONDS Procedure

This procedure sets the current session's Maximum Session Length in Seconds value, overriding the corresponding application attribute. This enables developers to dynamically shorten or lengthen the session life based on criteria determined after the user authenticates.

Syntax

```sql
APEX_UTIL.SET_SESSION_LIFETIME_SECONDS (
    p_seconds   IN NUMBER,
    p_scope     IN VARCHAR2 DEFAULT 'SESSION' );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_seconds` | A positive integer indicating the number of seconds that the session used by the application can exist. |
| `p_scope` | This parameter is obsolete. The procedure always sets the lifetime for the whole session. |

---

## SET_SESSION_MAX_IDLE_SECONDS Procedure

Sets the current application's Maximum Session Idle Time in Seconds value for the current session, overriding the corresponding application attribute. This allows developers to dynamically shorten or lengthen the maximum idle time allowed between page requests based on criteria determined after the user authenticates.

Syntax

```sql
APEX_UTIL.SET_SESSION_MAX_IDLE_SECONDS (
    p_seconds  IN    NUMEBER,
    p_scope    IN    VARCHAR2 DEFAULT 'SESSION' );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_seconds` | A positive integer indicating the number of seconds allowed between page requests. |
| `p_scope` | This parameter is obsolete. The procedure always sets the lifetime for the whole session. |

---

## SET_SESSION_SCREEN_READER_OFF Procedure

This procedure switches off screen reader mode for the current session.

Syntax

```sql
APEX_UTIL.SET_SESSION_SCREEN_READER_OFF;
```

Parameters

None

---

## SET_SESSION_SCREEN_READER_ON Procedure

This procedure puts the current session into screen reader mode.

Syntax

```sql
APEX_UTIL.SET_SESSION_SCREEN_READER_ON;
```

Parameters

None.

---

## SET_SESSION_STATE Procedure

This procedure sets session state for a current Oracle APEX session.

Syntax

```sql
APEX_UTIL.SET_SESSION_STATE (
    p_name     IN    VARCHAR2 DEFAULT NULL,
    p_value    IN    VARCHAR2 DEFAULT NULL
    p_commit   IN    BOOLEAN  DEFAULT TRUE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_name` | Name of the application-level or page-level item for which you are setting sessions state. |
| `p_value` | Value of session state to set. |
| `p_commit` | If TRUE (default), commit after modifying session state.  If FALSE or if the existing value in session state equals `p_value`, no commit.  This parameter is ignored when the application's Session State Changes attribute is set to `End Of Request`. |

---

## SET_SESSION_TERRITORY Procedure

This procedure sets the territory to be used for the current user in the current Oracle APEX session. The territory name must be a valid Oracle territory.

Syntax

```sql
APEX_UTIL.SET_SESSION_TERRITORY (
    p_territory IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_territory` | A valid Oracle territory name. Examples include: `AMERICA`, `UNITED KINGDOM`, `ISRAEL`, `AUSTRIA`, and `UNITED ARAB EMIRATES`. |

---

## SET_SESSION_TIME_ZONE Procedure

This procedure sets the time zone to be used for the current user in the current Oracle APEX session.

Syntax

```sql
APEX_UTIL.SET_SESSION_TIME_ZONE (
    p_time_zone IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_timezone` | A time zone value in the form of hours and minutes. Examples include: `+09:00`, `04:00`, `-05:00`. |

---

## SET_USERNAME Procedure

Note:

This procedure operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with APEX Accounts authentication.

This procedure updates a user account with a new `USER_NAME` value. To execute this procedure, the current user must have administrative privileges in the workspace.

Syntax

```sql
APEX_UTIL.SET_USERNAME (
    p_userid   IN NUMBER,
    p_username IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_userid` | The numeric ID of the user account. |
| `p_username` | `USER_NAME` value to be saved in the user account. |

---

## SET_WORKSPACE Procedure

This procedure sets the current workspace.

Syntax

```sql
APEX_UTIL.SET_WORKSPACE (
    p_workspace IN VARCHAR2 )
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_workspace` | The workspace's short name. |

---

## SHOW_HIGH_CONTRAST_MODE_TOGGLE Procedure

This procedure displays a link to the current page to turn on or off, toggle, the mode. For example, if you are in standard mode, this procedure returns a link that when clicked switches the high contrast mode on.

Syntax

```sql
APEX_UTIL.SHOW_HIGH_CONTRAST_MODE_TOGGLE (
    p_on_message  IN VARCHAR2 DEFAULT NULL,
    p_off_message IN VARCHAR2 DEFAULT NULL )
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_on_message` | Optional text used for the link to switch to high contrast mode when you are in standard mode. If this parameter is not passed, the default "Set High Contrast Mode On" text displays. |
| `p_off_message` | Optional text used for the link to switch to standard mode when you are in high contrast mode. If this parameter is not passed, the default "Set High Contrast Mode Off" text displays. |

---

## SHOW_SCREEN_READER_MODE_TOGGLE Procedure

This procedure displays a link to the current page to turn on or off (or toggle)
the mode. For example, if you are in standard mode, this procedure displays a link
that when clicked switches the screen reader mode on.

Syntax

```sql
APEX_UTIL.SHOW_SCREEN_READER_MODE_TOGGLE (
    p_on_message  IN VARCHAR2 DEFAULT NULL,
    p_off_message IN VARCHAR2 DEFAULT NULL )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_on_message` | Optional text used for the link to switch to screen reader mode, when you are in standard mode. If this parameter is not passed, the default 'Set Screen Reader Mode On' text is displayed. |
| `p_off_message` | Optional text used for the link to switch to standard mode, when you are in screen reader mode. If this parameter is not passed, the default 'Set Screen Reader Mode Off' text is displayed. |

---

## STRING_TO_TABLE Function (Deprecated)

Note:

This function is deprecated. Oracle recommends `APEX_STRING.STRING_TO_TABLE` instead.

See STRING_TO_TABLE Function.

Given a string, this function returns a PL/SQL array of type `APEX_APPLICATION_GLOBAL.VC_ARR2`. This array is a `VARCHAR2(32767)` table.

Syntax

```sql
APEX_UTIL.STRING_TO_TABLE (
    p_string       IN VARCHAR2,
    p_separator    IN VARCHAR2 DEFAULT ':' )
    RETURN APEX_APPLICATION_GLOBAL.VC_ARR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_string` | String to be converted into a PL/SQL table of type `APEX_APPLICATION_GLOBAL.VC_ARR2`. |
| `p_separator` | String separator. The default is a colon. |

---

## STRONG_PASSWORD_CHECK Procedure

This procedure returns Boolean `OUT` values based on whether a proposed password meets the password strength requirements as defined by the Oracle APEX site administrator.

Syntax

```sql
APEX_UTIL.STRONG_PASSWORD_CHECK (
    p_username                    IN  VARCHAR2,
    p_password                    IN  VARCHAR2,
    p_old_password                IN  VARCHAR2,
    p_workspace_name              IN  VARCHAR2,
    p_use_strong_rules            IN  BOOLEAN,
    p_min_length_err              OUT BOOLEAN,
    p_new_differs_by_err          OUT BOOLEAN,
    p_one_alpha_err               OUT BOOLEAN,
    p_one_numeric_err             OUT BOOLEAN,
    p_one_punctuation_err         OUT BOOLEAN,
    p_one_upper_err               OUT BOOLEAN,
    p_one_lower_err               OUT BOOLEAN,
    p_not_like_username_err       OUT BOOLEAN,
    p_not_like_workspace_name_err OUT BOOLEAN,
    p_not_like_words_err          OUT BOOLEAN,
    p_not_reusable_err            OUT BOOLEAN );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | Username that identifies the account in the current workspace. |
| `p_password` | Password to be checked against password strength rules. |
| `p_old_password` | Current password for the account. Used only to enforce "new password must differ from old" rule. |
| `p_workspace_name` | Current workspace name, used only to enforce "password must not contain workspace name" rule. |
| `p_use_strong_rules` | Pass `FALSE` when calling this API. |
| `p_min_length_err` | Result returns `TRUE` or `FALSE` depending upon whether the password meets minimum length requirement. |
| `p_new_differs_by_err` | Result returns `TRUE` or `FALSE` depending upon whether the password meets "new password must differ from old" requirements. |
| `p_one_alpha_err` | Result returns `TRUE` or `FALSE` depending upon whether the password meets requirement to contain at least one alphabetic character. |
| `p_one_numeric_err` | Result returns `TRUE` or `FALSE` depending upon whether the password meets requirements to contain at least one numeric character. |
| `p_one_punctuation_err` | Result returns `TRUE` or `FALSE` depending upon whether the password meets requirements to contain at least one punctuation character. |
| `p_one_upper_err` | Result returns `TRUE` or `FALSE` depending upon whether the password meets requirements to contain at least one upper-case character. |
| `p_one_lower_err` | Result returns `TRUE` or `FALSE` depending upon whether the password meets requirements to contain at least one lower-case character. |
| `p_not_like_username_err` | Result returns `TRUE` or `FALSE` depending upon whether the password meets requirements that it must not contain the username. |
| `p_not_like_workspace_name_err` | Result returns `TRUE` or `FALSE` depending upon whether the password meets requirements that it must not contain the workspace name. |
| `p_not_like_words_err` | Result returns `TRUE` or `FALSE` whether the password meets requirements that it must not contain specified simple words. |
| `p_not_reusable_err` | Result returns `TRUE` or `FALSE` whether the password can be reused based on password history rules. |

---

## STRONG_PASSWORD_VALIDATION Function

This function returns formatted HTML in a VARCHAR2 result based on whether a proposed password meets the password strength requirements as defined by the Oracle APEX site administrator.

Syntax

```sql
APEX_UTIL.STRONG_PASSWORD_VALIDATION (
    p_username          IN  VARCHAR2,
    p_password          IN  VARCHAR2,
    p_old_password      IN  VARCHAR2 DEFAULT NULL,
    p_workspace_name    IN  VARCHAR2 )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_username` | Username that identifies the account in the current workspace. |
| `p_password` | Password to be checked against password strength rules. |
| `p_old_password` | Current password for the account. Used only to enforce "new password must differ from old" rule. |
| `p_workspace_name` | Current workspace name, used only to enforce "password must not contain workspace name" rule. |

---

## SUBMIT_FEEDBACK Procedure

This procedure enables you to write a procedure to submit feedback, rather than using the feedback page generated by Create Page Wizard.

Syntax

```sql
APEX_UTIL.SUBMIT_FEEDBACK (
    p_comment          IN VARCHAR2 DEFAULT NULL,
    p_type             IN NUMBER   DEFAULT '1',
    p_application_id   IN VARCHAR2 DEFAULT NULL,
    p_page_id          IN VARCHAR2 DEFAULT NULL,
    p_email            IN VARCHAR2 DEFAULT NULL,
    p_screen_width     IN VARCHAR2 DEFAULT NULL,
    p_screen_height    IN VARCHAR2 DEFAULT NULL,
    p_attribute_01     IN VARCHAR2 DEFAULT NULL,
    p_attribute_02     IN VARCHAR2 DEFAULT NULL,
    p_attribute_03     IN VARCHAR2 DEFAULT NULL,
    p_attribute_04     IN VARCHAR2 DEFAULT NULL,
    p_attribute_05     IN VARCHAR2 DEFAULT NULL,
    p_attribute_06     IN VARCHAR2 DEFAULT NULL,
    p_attribute_07     IN VARCHAR2 DEFAULT NULL,
    p_attribute_08     IN VARCHAR2 DEFAULT NULL,
    p_label_01         IN VARCHAR2 DEFAULT NULL,
    p_label_02         IN VARCHAR2 DEFAULT NULL,
    p_label_03         IN VARCHAR2 DEFAULT NULL,
    p_label_04         IN VARCHAR2 DEFAULT NULL,
    p_label_05         IN VARCHAR2 DEFAULT NULL,
    p_label_06         IN VARCHAR2 DEFAULT NULL,
    p_label_07         IN VARCHAR2 DEFAULT NULL,
    p_label_08         IN VARCHAR2 DEFAULT NULL,
    p_rating           IN NUMBER   DEFAULT NULL,
    p_attachment_name  IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_comment` | Comment to be submitted. |
| `p_type` | Type of feedback (1 is General Comment, 2 is Enhancement Request, 3 is Bug). |
| `p_application_id` | ID of application related to the feedback. |
| `p_page_id` | ID of page related to the feedback. |
| `p_email` | Email of the user providing the feedback. |
| `p_screen_width` | Width of screen at time feedback was provided. |
| `p_screen_height` | Height of screen at time feedback was provided. |
| `p_attribute_01` | Custom attribute for collecting feedback. |
| `p_attribute_02` | Custom attribute for collecting feedback. |
| `p_attribute_03` | Custom attribute for collecting feedback. |
| `p_attribute_04` | Custom attribute for collecting feedback. |
| `p_attribute_05` | Custom attribute for collecting feedback. |
| `p_attribute_06` | Custom attribute for collecting feedback. |
| `p_attribute_07` | Custom attribute for collecting feedback. |
| `p_attribute_08` | Custom attribute for collecting feedback. |
| `p_label_01` | Label for corresponding custom attribute. |
| `p_label_02` | Label for corresponding custom attribute. |
| `p_label_03` | Label for corresponding custom attribute. |
| `p_label_04` | Label for corresponding custom attribute. |
| `p_label_05` | Label for corresponding custom attribute. |
| `p_label_06` | Label for corresponding custom attribute. |
| `p_label_07` | Label for corresponding custom attribute. |
| `p_label_08` | Label for corresponding custom attribute. |
| `p_rating` | User experience (3 is Good, 2 is Neutral, 1 is Bad). |
| `p_attachment_name` | Bind variable reference to the feedback form's "File Browse" page item. |

---

## SUBMIT_FEEDBACK_FOLLOWUP Procedure

This procedure enables you to submit follow up to a feedback.

Syntax

```sql
APEX_UTIL.SUBMIT_FEEDBACK_FOLLOWUP (
    p_feedback_id      IN NUMBER,
    p_follow_up        IN VARCHAR2 DEFAULT NULL,
    p_email            IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_feedback_id` | ID of feedback that this is a follow up to. |
| `p_follow_up` | Text of follow up. |
| `p_email` | Email of user providing the follow up. |

---

## TABLE_TO_STRING Function (Deprecated)

Note:

This function is deprecated. Oracle recommends using the `JOIN` and `JOIN_CLOB` functions instead.

Given a a PL/SQL table of type `APEX_APPLICATION_GLOBAL.VC_ARR2`, this function returns a delimited string separated by the supplied separator, or by the default separator, a colon (:).

Syntax

```sql
APEX_UTIL.TABLE_TO_STRING (
    p_table     IN      apex_application_global.vc_arr2,
    p_string    IN      VARCHAR2 DEFAULT ':' )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_string` | String separator. Default separator is a colon (:). |
| `p_table` | PL/SQL table that is to be converted into a delimited string. |

---

## UNEXPIRE_END_USER_ACCOUNT Procedure

Note:

This procedure operates on the native Oracle APEX user accounts repository and is only applicable to applications configured with APEX Accounts authentication.

This procedure makes expired end users accounts and the associated passwords usable, enabling an end user to log into developed applications.

Syntax

```sql
APEX_UTIL.UNEXPIRE_END_USER_ACCOUNT (
    p_user_name IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## UNEXPIRE_WORKSPACE_ACCOUNT Procedure

This procedure unexpires developer and workspace administrator accounts and the associated passwords, enabling the developer or administrator to log into a workspace.

Syntax

```sql
APEX_UTIL.UNEXPIRE_WORKSPACE_ACCOUNT (
    p_user_name IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## UNLOCK_ACCOUNT Procedure

This procedure sets a user account status to unlocked. Must be run by an authenticated workspace administrator in a page request context.

Syntax

```sql
APEX_UTIL.UNLOCK_ACCOUNT (
    p_user_name IN VARCHAR2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |

---

## URL_ENCODE Function (Deprecated)

Note:

This API is deprecated and will be
removed in a future release.

Use the UTL_URL.ESCAPE function instead.

The following special characters are encoded as follows:

```sql
 Special       After
Characters    Encoding
    %          %25
    +          %2B
  space         +
    .          %2E
    *          %2A
    ?          %3F
    \          %5C
    /          %2F
    >          %3E
    <          %3C
    }          %7B
    {          %7D
    ~          %7E
    [          %5B
    ]          %5D
    ;          %3B
    ?          %3F
    @          %40
    &          %26
    #          %23
    |          %7C
    ^          %5E
    :          %3A
    =          %3D
    $          %24
```

Syntax

```sql
APEX_UTIL.URL_ENCODE (
    p_url   IN    VARCHAR2)
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_url` | The string to be encoded. |

---

## WORKSPACE_ACCOUNT_DAYS_LEFT Function

This function returns the number of days remaining before the developer or workspace administrator account password expires. Any authenticated user can run this function in a page request context.

Syntax

```sql
APEX_UTIL.WORKSPACE_ACCOUNT_DAYS_LEFT (
    p_user_name IN VARCHAR2 )
RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_user_name` | The user name of the user account. |