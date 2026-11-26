<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_DEBUG (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_DEBUG

The `APEX_DEBUG` package provides utility functions for managing the debug message log. Specifically, this package provides the necessary APIs to instrument and debug PL/SQL code contained within your Oracle APEX application as well as PL/SQL code in database stored procedures and functions. Instrumenting your PL/SQL code makes it much easier to track down bugs and isolate unexpected behavior more quickly.

The package also provides the means to enable and disable debugging at different debug levels and utility procedures to clean up the message log.

You can view the message log either as described in the Accessing Debugging Mode section of the Oracle APEX App Builder
User’s Guide or by querying the `APEX_DEBUG_MESSAGES` view.

For further information, see the individual API descriptions.

Note:

In APEX release 4.2, the APEX_DEBUG_MESSAGE package was renamed to APEX_DEBUG. The APEX_DEBUG_MESSAGE package name is still supported to provide backward compatibility. As a best practice, however, use the new APEX_DEBUG package for new applications unless you plan to run them in an earlier version of APEX.


See Also:

Accessing Debugging Mode in Oracle APEX App Builder
User’s Guide

---

## Constants

The APEX_DEBUG package uses the following constants.

```sql
subtype t_log_level is pls_integer;
c_log_level_error constant t_log_level := 1;
    -- critical error
c_log_level_warn constant t_log_level := 2;
    -- less critical error
c_log_level_info constant t_log_level := 4;
    -- default level if debugging is enabled
    -- (for example, used by apex_application.debug)
c_log_level_app_enter constant t_log_level := 5;
    -- application: messages when procedures/functions are entered
c_log_level_app_trace constant t_log_level := 6;
    -- application: other messages within procedures/functions
c_log_level_engine_enter constant t_log_level := 8;
    -- APEX engine: messages when procedures/functions are entered
c_log_level_engine_trace constant t_log_level := 9;
    -- APEX engine: other messages within procedures/functions
```

---

## DISABLE Procedure

This procedure turns off debug messaging.

Syntax

```sql
APEX_DEBUG.DISABLE;
```

Parameters

None.

---

## DISABLE_DBMS_OUTPUT Procedure

This procedure stops writing all debug logs with `dbms_output`.

Syntax

```sql
DISABLE_DBMS_OUTPUT;
```

Parameters

None.

---

## ENABLE Procedure

This procedure turns on debug messaging. You can specify the types of debug messages that are logged by level of importance.

Note:

You only need to call `ENABLE` procedure once per page view or page accept.

Syntax

```sql
APEX_DEBUG.ENABLE (
    p_level    IN  t_log_level DEFAULT c_log_level_info )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_level` | Level or levels of messages to log. Must be an integer from 1 to 9, where level 1 is the most important messages and level 4 (the default) is the least important. Setting to a specific level logs messages both at that level and below that level. For example, setting `p_level` to 2 logs any message at level 1 and 2. |

---

## ENTER Procedure

This procedure logs messages at level `c_log_level_app_enter`. Use `APEX_DEBUG.ENTER()` to log the routine name and its arguments at the beginning of a procedure or function.

Syntax

```sql
APEX_DEBUG.ENTER (
    p_routine_name      IN VARCHAR2,
    p_name01            IN VARCHAR2     DEFAULT NULL,
    p_value01           IN VARCHAR2     DEFAULT NULL,
    p_name02            IN VARCHAR2     DEFAULT NULL,
    p_value02           IN VARCHAR2     DEFAULT NULL,
    p_name03            IN VARCHAR2     DEFAULT NULL,
    p_value03           IN VARCHAR2     DEFAULT NULL,
    p_name04            IN VARCHAR2     DEFAULT NULL,
    p_value04           IN VARCHAR2     DEFAULT NULL,
    p_name05            IN VARCHAR2     DEFAULT NULL,
    p_value05           IN VARCHAR2     DEFAULT NULL,
    p_name06            IN VARCHAR2     DEFAULT NULL,
    p_value06           IN VARCHAR2     DEFAULT NULL,
    p_name07            IN VARCHAR2     DEFAULT NULL,
    p_value07           IN VARCHAR2     DEFAULT NULL,
    p_name08            IN VARCHAR2     DEFAULT NULL,
    p_value08           IN VARCHAR2     DEFAULT NULL,
    p_name09            IN VARCHAR2     DEFAULT NULL,
    p_value09           IN VARCHAR2     DEFAULT NULL,
    p_name10            IN VARCHAR2     DEFAULT NULL,
    p_value10           IN VARCHAR2     DEFAULT NULL,
    p_value_max_length  IN PLS_INTEGER  DEFAULT 1000 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_routine_name` | The name of the procedure or function. |
| `p_namexx`/`p_valuexx` | The procedure or function parameter name and value. |
| `p_value_max_length` | The `p_valuexx` values is truncated to this length. The tilde (`~`) character is appended to indicate that the original value exceeded this length. |

---

## ENABLE_DBMS_OUTPUT Procedure

This procedure writes all debug logs via `dbms_output`. If debug is disabled, this call also enables it with log level `c_log_level_warn`. You have to set a debug level higher than `c_log_level_warn` for finer grained debug output. The output `95` starts with a configurable prefix, followed by the log level, `"|"` and the actual debug message.

Syntax

```sql
ENABLE_DBMS_OUTPUT (
    p_prefix    IN VARCHAR2    DEFAULT '# APEX|' )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_prefix` | Prefix for lines that go to `dbms_output`, default `'# APEX|'`. |

---

## ERROR Procedure

This procedure logs messages at level `c_log_level_error`. This procedure always logs, even if debug mode is turned off.

Syntax

```sql
APEX_DEBUG.ERROR (
    p_message       IN VARCHAR2,
    p0              IN VARCHAR2     DEFAULT NULL,
    p1              IN VARCHAR2     DEFAULT NULL,
    p2              IN VARCHAR2     DEFAULT NULL,
    p3              IN VARCHAR2     DEFAULT NULL,
    p4              IN VARCHAR2     DEFAULT NULL,
    p5              IN VARCHAR2     DEFAULT NULL,
    p6              IN VARCHAR2     DEFAULT NULL,
    p7              IN VARCHAR2     DEFAULT NULL,
    p8              IN VARCHAR2     DEFAULT NULL,
    p9              IN VARCHAR2     DEFAULT NULL,
    p_max_length    IN PLS_INTEGER  DEFAULT 1000 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_message` | The debug message. Occurrences of `%` are replaced by `p0` to `p19`, as in `utl_lms.format_message` and C's sprintf. Occurrences of `%%` represent the special character `%`. Occurrences of `%<n>` are replaced by `p<n>`. |
| `p0` through `p9` | Substitution strings for `%` placeholders. |
| `p_max_length` | The `p<n>` values are truncated to this length. |

---

## GET_LAST_MESSAGE_ID Function

This function returns the identifier for the last debug message that was generated in this session. The value is null until the first debug message has been generated.

Syntax

```sql
APEX_DEBUG.GET_LAST_MESSAGE_ID (
  RETURN NUMBER );
```

---

## GET_PAGE_VIEW_ID Function

This function returns the current page view identifier, which is a unique ID for each browser request or standalone database session. The value is null until the first debug message has been generated.

Syntax

```sql
APEX_DEBUG.GET_PAGE_VIEW_ID (
  RETURN NUMBER );
```

---

## INFO Procedure

This procedure logs messages at level `c_log_level_info`.

Syntax

```sql
APEX_DEBUG.INFO (
    p_message       IN VARCHAR2,
    p0              IN VARCHAR2     DEFAULT NULL,
    p1              IN VARCHAR2     DEFAULT NULL,
    p2              IN VARCHAR2     DEFAULT NULL,
    p3              IN VARCHAR2     DEFAULT NULL,
    p4              IN VARCHAR2     DEFAULT NULL,
    p5              IN VARCHAR2     DEFAULT NULL,
    p6              IN VARCHAR2     DEFAULT NULL,
    p7              IN VARCHAR2     DEFAULT NULL,
    p8              IN VARCHAR2     DEFAULT NULL,
    p9              IN VARCHAR2     DEFAULT NULL,
    p_max_length    IN PLS_INTEGER  DEFAULT 1000 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_message` | The debug message. Occurrences of `%` are replaced by `p0` to `p19`, as in `utl_lms.format_message` and C's sprintf. Occurrences of `%%` represent the special character `%`. Occurrences of `%<n>` are replaced by `p<n>`. |
| `p0` through `p9` | Substitution strings for `%` placeholders. |
| `p_max_length` | The `p<n>` values are truncated to this length. The tilde (`~`) character is appended to indicate that the original value exceeded this length. |

---

## LOG_DBMS_OUTPUT Procedure

This procedure writes the contents of `dbms_output.get_lines` to the debug log. Messages of legacy applications which use `dbms_output` are copied into the debug log. In order to write to the debug log, `dbms_output.enable` must be performed

Syntax

```sql
APEX_DEBUG.LOG_DBMS_OUTPUT;
```

Parameters

None.

---

## LOG_LONG_MESSAGE Procedure

This procedure emits debug messages from PL/SQL components of Oracle APEX, or PL/SQL procedures and functions.

This procedure is the same as LOG_MESSAGE, except it allows logging of much longer messages, which are subsequently split into 4,000 character chunks in the debugging output (because a single debug message is constrained to 4,000 characters).

Note:

As a best practice, Oracle recommends using shorter message APIs when possible (ERROR, WARN, and so on), and reserving LOG_LONG_MESSAGE for scenarios that require longer messages.

Syntax

```sql
APEX_DEBUG.LOG_LONG_MESSAGE (
    p_message   IN VARCHAR2     DEFAULT NULL,
    p_enabled   IN BOOLEAN      DEFAULT FALSE,
    p_level     IN t_log_level  DEFAULT c_log_level_app_trace )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_message` | Log long message with maximum size of 32,767 bytes. |
| `p_enabled` | Set to `TRUE` to always log messages, irrespective of whether debugging is enabled. Set to `FALSE` to only log messages if debugging is enabled. |
| p_level | Identifies the level of the long log message. See Constants. |

---

## LOG_MESSAGE Procedure (Deprecated)

This procedure logs a debug message.

Note:

This API is deprecated and will be
removed in a future release.

Instead of this procedure, use the following:

* ERROR Procedure
* WARN Procedure
* MESSAGE Procedure
* INFO Procedure
* ENTER Procedure
* TRACE Procedure

Syntax

```sql
APEX_DEBUG.LOG_MESSAGE (
    p_message   IN  VARCHAR2    DEFAULT NULL,
    p_enabled   IN  BOOLEAN     DEFAULT FALSE,
    p_level     IN  t_log_level DEFAULT c_log_level_app_trace )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_message` | The debug message with a maximum length of 1,000 bytes. |
| `p_enabled` | Messages are logged when logging is enabled. `TRUE` enables logging. |
| `p_level` | Identifies the level of the log message where `1` is most important and `9` is least important. This is an integer value. |

---

## LOG_PAGE_SESSION_STATE Procedure

This procedure logs the session's item values.

Syntax

```sql
APEX_DEBUG.LOG_PAGE_SESSION_STATE (
    p_page_id   IN  NUMBER      DEFAULT NULL,
    p_enabled   IN  BOOLEAN     DEFAULT FALSE,
    p_level     IN  t_log_level DEFAULT c_log_level_app_trace )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_page_id` | Identifies a page within the current applicaton and workspace context. |
| `p_enabled` | Messages are logged when logging is enabled. `TRUE` enables logging. |
| `p_level` | Identifies the level of the log message where `1` is most important, `9` is least important. Must be an integer value. |

---

## MESSAGE Procedure

This procedure logs a formatted debug message, general version.

Syntax

```sql
APEX_DEBUG.MESSAGE (
    p_message       IN VARCHAR2,
    p0              IN VARCHAR2     DEFAULT NULL,
    p1              IN VARCHAR2     DEFAULT NULL,
    p2              IN VARCHAR2     DEFAULT NULL,
    p3              IN VARCHAR2     DEFAULT NULL,
    p4              IN VARCHAR2     DEFAULT NULL,
    p5              IN VARCHAR2     DEFAULT NULL,
    p6              IN VARCHAR2     DEFAULT NULL,
    p7              IN VARCHAR2     DEFAULT NULL,
    p8              IN VARCHAR2     DEFAULT NULL,
    p9              IN VARCHAR2     DEFAULT NULL,
    p10             IN VARCHAR2     DEFAULT NULL,
    p11             IN VARCHAR2     DEFAULT NULL,
    p12             IN VARCHAR2     DEFAULT NULL,
    p13             IN VARCHAR2     DEFAULT NULL,
    p14             IN VARCHAR2     DEFAULT NULL,
    p15             IN VARCHAR2     DEFAULT NULL,
    p16             IN VARCHAR2     DEFAULT NULL,
    p17             IN VARCHAR2     DEFAULT NULL,
    p18             IN VARCHAR2     DEFAULT NULL,
    p19             IN VARCHAR2     DEFAULT NULL,
    p_max_length    IN PLS_INTEGER  DEFAULT 1000,
    p_level         IN t_log_level  DEFAULT c_log_level_info,
    p_force         IN BOOLEAN      DEFAULT FALSE )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_message` | The debug message. Occurrences of `%` are replaced by `p0` to `p19`, as in `utl_lms.format_message` and C's sprintf. Occurrences of `%%` represent the special character `%`. Occurrences of `%<n>` are replaced by `p<n>`. |
| `p0` through `p19` | Substitution strings for `%` placeholders. |
| `p_max_length` | The `p<n>` values is truncated to this length. The tilde (`~`) character is appended to indicate that the original value exceeded this length. |
| `p_level` | The log level for the message, default is `c_log_level_info`. See Constants. |
| `p_force` | If `TRUE`, this generates a debug message even if the page is not rendered in debug mode or `p_level` is greater than the configured debug messaging (using the URL or using the enable procedure). |

---

## REMOVE_DEBUG_BY_AGE Procedure

Deletes all data older than the specified number of days from the debug message log.

Syntax

```sql
APEX_DEBUG.REMOVE_DEBUG_BY_AGE (
    p_application_id    IN NUMBER,
    p_older_than_days   IN NUMBER )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The application ID of the application. |
| `p_older_than_days` | The number of days data can exist in the debug message log before it is deleted. |

---

## REMOVE_DEBUG_BY_APP Procedure

Deletes all data belonging to a specified application from the debug message log.

Syntax

```sql
APEX_DEBUG.REMOVE_DEBUG_BY_APP (
    p_application_id    IN NUMBER )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The application ID of the application. |

---

## REMOVE_DEBUG_BY_VIEW Procedure

Deletes all data for a specified view from the message log.

Syntax

```sql
APEX_DEBUG.REMOVE_DEBUG_BY_VIEW (
    p_application_id    IN NUMBER,
    p_view_id           IN NUMBER )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_application_id` | The application ID of the application. |
| `p_view_id` | The view ID of the view. |

---

## REMOVE_SESSION_MESSAGES Procedure

This procedure deletes from the debug message log all data for a given session in your workspace defaults to your current session.

Syntax

```sql
APEX_DEBUG.REMOVE_SESSION_MESSAGES (
    p_session    IN NUMBER  DEFAULT NULL )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_session` | The session ID. Defaults to your current session. |

---

## TOCHAR Function

This procedure converts a BOOLEAN to a VARCHAR2.

Syntax

```sql
APEX_DEBUG.TOCHAR (
    p_value IN BOOLEAN )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | A BOOLEAN `0` or `1` that is converted to `FALSE` or `TRUE` respectively. |

---

## TRACE Procedure

This procedure logs messages at level `c_log_level_app_trace`.

Syntax

```sql
APEX_DEBUG.TRACE (
    p_message       IN  VARCHAR2,
    p0              IN  VARCHAR2    DEFAULT NULL,
    p1              IN  VARCHAR2    DEFAULT NULL,
    p2              IN  VARCHAR2    DEFAULT NULL,
    p3              IN  VARCHAR2    DEFAULT NULL,
    p4              IN  VARCHAR2    DEFAULT NULL,
    p5              IN  VARCHAR2    DEFAULT NULL,
    p6              IN  VARCHAR2    DEFAULT NULL,
    p7              IN  VARCHAR2    DEFAULT NULL,
    p8              IN  VARCHAR2    DEFAULT NULL,
    p9              IN  VARCHAR2    DEFAULT NULL,
    p_max_length    IN  PLS_INTEGER DEFAULT 1000 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_message` | The debug message. Occurrences of `%` are replaced by `p0` to `p19`, as in `utl_lms.format_message` and C's sprintf. Occurrences of `%%` represent the special character `%`. Occurrences of `%<n>` are replaced by `p<n>`. |
| `p0` through `p9` | Substitution strings for `%` placeholders. |
| `p_max_length` | The `p<n>` values are truncated to this length. The tilde (`~`) character is appended to indicate that the original value exceeded this length. |

---

## WARN Procedure

This procedure logs messages at level `c_log_level_warn`.

Syntax

```sql
APEX_DEBUG.WARN (
    p_message       IN VARCHAR2,
    p0              IN VARCHAR2     DEFAULT NULL,
    p1              IN VARCHAR2     DEFAULT NULL,
    p2              IN VARCHAR2     DEFAULT NULL,
    p3              IN VARCHAR2     DEFAULT NULL,
    p4              IN VARCHAR2     DEFAULT NULL,
    p5              IN VARCHAR2     DEFAULT NULL,
    p6              IN VARCHAR2     DEFAULT NULL,
    p7              IN VARCHAR2     DEFAULT NULL,
    p8              IN VARCHAR2     DEFAULT NULL,
    p9              IN VARCHAR2     DEFAULT NULL,
    p_max_length    IN PLS_INTEGER  DEFAULT 1000 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_message` | The debug message. Occurrences of `%` are replaced by `p0` to `p19`, as in `utl_lms.format_message` and C's sprintf. Occurrences of `%%` represent the special character `%`. Occurrences of `%<n>` are replaced by `p<n>`. |
| `p0` through `p9` | Substitution strings for `%` placeholders. |
| `p_max_length` | The `p<n>` values are truncated to this length. The tilde (`~`) character is appended to indicate that the original value exceeded this length. |