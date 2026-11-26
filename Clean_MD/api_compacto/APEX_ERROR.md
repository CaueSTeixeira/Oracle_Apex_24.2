<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_ERROR (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_ERROR

The APEX_ERROR package provides the interface declarations and utility functions for an error handling function and includes procedures and functions to raise errors in an APEX application.

---

## Constants and Attributes Used for Result Types

The following constants are used for the API parameter `p_display_location` and the attribute `display_location` in the `t_error` and `t_error_result` types.

```sql
c_inline_with_field            constant varchar2(40):='INLINE_WITH_FIELD';
c_inline_with_field_and_notif  constant varchar2(40):='INLINE_WITH_FIELD_AND_NOTIFICATION';
c_inline_in_notification       constant varchar2(40):='INLINE_IN_NOTIFICATION';
c_on_error_page                constant varchar2(40):='ON_ERROR_PAGE';
```

The following constants are used for the API parameter `associated_type` in the `t_error` type.

```sql
c_ass_type_page_item           constant varchar2(30):='PAGE_ITEM';
c_ass_type_region              constant varchar2(30):='REGION';
c_ass_type_region_column       constant varchar2(30):='REGION_COLUMN';
```

The following record structure is passed into an error handling callout function and contains all the relevant information about the error.

```sql
type t_error is record (
    message                 varchar2(32767),
        /* Error message which will be displayed */
    additional_info         varchar2(32767),
        /* Only used for display_location ON_ERROR_PAGE to display additional error information */
    display_location        varchar2(40),
        /* Use constants "used for display_location" below */
    association_type        varchar2(40),
        /* Use constants "used for asociation_type" below */
    page_item_name          varchar2(255),
        /* Associated page item name */
    region_id               number,
        /* Associated tabular form region id of the primary application */
    column_alias            varchar2(255),
        /* Associated tabular form column alias */
    row_num                 pls_integer,
        /* Associated tabular form row */
    apex_error_code         varchar2(255),
        /* Contains the system message code if it's an error raised by APEX */
    is_internal_error       boolean,
        /* Set to TRUE if it's a critical error raised by the APEX engine, like an invalid SQL/PLSQL statements,
        ... Internal Errors are always displayed on the Error Page */
    is_common_runtime_error boolean,
        /* TRUE for internal authorization, session and session state errors that normally should not be masked
        by an error handler */
    ora_sqlcode             number,
        /* SQLCODE on exception stack which triggered the error, NULL if the error was not raised by an ORA error */
    ora_sqlerrm             varchar2(32767),
        /* SQLERRM which triggered the error, NULL if the error was not raised by an ORA error */
    error_backtrace         varchar2(32767),
        /* Output of sys.dbms_utility.format_error_backtrace or sys.dbms_utility.format_call_stack */
    error_statement         varchar2(32767),
        /* Statement that was parsed when the error occurred - only suitable when parsing caused the error */
    component               apex_application.t_component,
        /* Component which has been processed when the error occurred */
);
```

The following record structure must be returned by an error handling callout function.

```sql
type t_error_result is record (
    message             varchar2(32767),  /* Error message which will be displayed */
    additional_info     varchar2(32767),  /* Only used for display_location ON_ERROR_PAGE
                                          to display additional error information */
    display_location    varchar2(40),     /* Use constants "used for display_location" below */
    page_item_name      varchar2(255),    /* Associated page item name */
    column_alias        varchar2(255)     /* Associated tabular form column alias */
);
```

---

## Example of an Error Handling Function

The following is an example of an error handling function.

```sql
create or replace function apex_error_handling_example (
    p_error in apex_error.t_error )
    return apex_error.t_error_result
IS
    l_result          apex_error.t_error_result;
    l_reference_id    number;
    l_constraint_name varchar2(255);
BEGIN
    l_result := apex_error.init_error_result (
                    p_error => p_error );

    -- If it's an internal error raised by APEX, like an invalid statement or
    -- code which can't be executed, the error text might contain security
    -- sensitive information. To avoid this security problem we can rewrite the
    -- error to a generic error message and log the original error message for
    -- further investigation by the help desk.

    IF p_error.is_internal_error THEN

        -- mask all errors that are not common runtime errors (Access Denied
        -- errors raised by application / page authorization and all errors
        -- regarding session and session state)

        IF not p_error.is_common_runtime_error THEN

            -- log error for example with an autonomous transaction and return
            -- l_reference_id as reference#
            -- l_reference_id := log_error (
            --                       p_error => p_error );

            -- Change the message to the generic error message which doesn't
            -- expose any sensitive information.

            l_result.message    := 'An unexpected internal application
                                error has occurred. '||
                                'Please get in contact with XXX and provide '||
                                'reference#
                                '||to_char(l_reference_id, '999G999G999G990')||
                                ' for further investigation.';
            l_result.additional_info := null;
        END IF;
    ELSE

        -- Note: If you want to have friendlier ORA error messages, you can
        -- also define a text message with the name pattern
        --
        --      APEX.ERROR.ORA-number
        --
        -- There is no need to implement custom code for that.

        -- If it's a constraint violation like
        --
        --   -) ORA-00001: unique constraint violated
        --   -) ORA-02091: transaction rolled back (-> can hide a deferred
        --      constraint)
        --   -) ORA-02290: check constraint violated
        --   -) ORA-02291: integrity constraint violated - parent key not
        --      found
        --   -) ORA-02292: integrity constraint violated - child record found
        --
        -- We try to get a friendly error message from our constraint lookup
        -- configuration. If we don't find the constraint in our lookup table,
        -- we fallback to the original ORA error message.

        IF p_error.ora_sqlcode in (-1, -2091, -2290, -2291, -2292) THEN
            l_constraint_name := apex_error.extract_constraint_name (
                                     p_error => p_error );

            BEGIN
                select message
                  into l_result.message
                  from constraint_lookup
                 where constraint_name = l_constraint_name;
            EXCEPTION when no_data_found THEN null;

            -- Not every constraint has to be in our lookup table.

            END;
        END IF;

        -- If an ORA error has been raised, for example a
        -- raise_application_error(-20xxx, '...') in a table trigger or in a
        -- PL/SQL package called by a process and we haven't found the error
        -- in our lookup table, then we just want to see the actual error text
        -- and not the full error stack with all the ORA error numbers.

        IF p_error.ora_sqlcode is not null and l_result.message =
        p_error.message THEN
            l_result.message := apex_error.get_first_ora_error_text (
                                    p_error => p_error );
        END IF;

        -- If no associated page item/tabular form column has been set, we can
        -- use apex_error.auto_set_associated_item to automatically guess the
        -- affected error field by examine the ORA error for constraint names
        -- or column names.

        IF l_result.page_item_name is null and l_result.column_alias is null
        THEN
            apex_error.auto_set_associated_item (
                p_error        => p_error,
                p_error_result => l_result );
        END IF;
    END IF;

    RETURN l_result;
END apex_error_handling_example;
```

---

## ADD_ERROR Procedure Signature 1

This procedure adds an error message to the error stack that is used to display an error on an error page or inline in a notification. It can be called in a validation or process to add one or more errors to the error stack.

Note:

This procedure must be called before the Oracle APEX application has performed the last validation or process. Otherwise, the error is ignored if it does not have a display location of `apex_error.c_on_error_page`.

Syntax

```sql
APEX_ERROR.ADD_ERROR (
    p_message          IN VARCHAR2,
    p_additional_info  IN VARCHAR2 DEFAULT NULL,
    p_display_location IN VARCHAR2,
    p_ignore_ora_error IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_message` | Displayed error message. |
| `p_additional_info` | Additional error information needed if the error is displayed on the error page. |
| `p_display_location` | Specifies where the error message is displayed. Use the constant `apex_error.c_inline_in_notification` or `apex_error.c_on_error_page`. See Constants and Attributes Used for Result Types. |
| `p_ignore_ora_error` | If `FALSE` (default), retains the original error in the error stack. If `TRUE` and `add_error` is called from an exception handler, removes the original error that caused the exception from the error stack. |

---

## ADD_ERROR Procedure Signature 2

This procedure adds an error message to the error stack that is used to display an error for a page item inline in a notification. It can be called in a validation or process to add one or more errors to the error stack.

Note:

This procedure must be called before the APEX application has performed the last validation or process. Otherwise, the error is ignored if it does not have a display location of `apex_error.c_on_error_page`.

Syntax

```sql
APEX_ERROR.ADD_ERROR (
    p_message          IN VARCHAR2,
    p_additional_info  IN VARCHAR2 DEFAULT NULL,
    p_display_location IN VARCHAR2,
    p_page_item_name   IN VARCHAR2,
    p_ignore_ora_error IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_message` | Displayed error message. |
| `p_additional_info` | Additional error information needed if the error is displayed on the error page. |
| `p_display_location` | Specifies where the error message is displayed. Use the constant `apex_error.c_inline_with_field` or `apex_error.c_inline_with_field_and_notif`. See Constants and Attributes Used for Result Types. |
| `p_page_item_name` | Name of the page item on the current page that is highlighted if `apex_error.c_inline_with_field` or `apex_error.c_inline_with_field_and_notif` are used as the display location. |
| `p_ignore_ora_error` | If `FALSE` (default), retains the original error in the error stack. If `TRUE` and `add_error` is called from an exception handler, removes the original error that caused the exception from the error stack. |

---

## ADD_ERROR Procedure Signature 3

Adds an error message to the error stack based on a text message defined in Shared Components. This error message can be displayed in all display locations. It can be called in a validation or process to add one or more errors to the error stack.

Note:

This procedure must be called before the Oracle APEX application has performed the last validation or process. Otherwise, the error is ignored if it does not have a display location of `apex_error.c_on_error_page`.

Syntax

```sql
APEX_ERROR.ADD_ERROR (
    p_error_code          IN VARCHAR2,
    p0                    IN VARCHAR2 DEFAULT NULL,
    p1                    IN VARCHAR2 DEFAULT NULL,
    p2                    IN VARCHAR2 DEFAULT NULL,
    p3                    IN VARCHAR2 DEFAULT NULL,
    p4                    IN VARCHAR2 DEFAULT NULL,
    p5                    IN VARCHAR2 DEFAULT NULL,
    p6                    IN VARCHAR2 DEFAULT NULL,
    p7                    IN VARCHAR2 DEFAULT NULL,
    p8                    IN VARCHAR2 DEFAULT NULL,
    p9                    IN VARCHAR2 DEFAULT NULL,
    p_escape_placeholders IN BOOLEAN  DEFAULT TRUE,
    p_additional_info     IN VARCHAR2 DEFAULT NULL,
    p_display_location    IN VARCHAR2,
    p_page_item_name      IN VARCHAR2,
    p_ignore_ora_error    IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_error_code` | Name of shared component text message. |
| `p_additional_info` | Additional error information needed if the error is displayed on the error page. |
| `p0` through `p9` | Values for %0 through %9 placeholders defined in the text message. |
| `p_escape_placeholders` | If set to `TRUE`, the values provided in `p0` through `p9` are escaped with `sys.htf.escape_sc` before replacing the placeholder in the text message. If set to `FALSE`, values are not escaped. |
| `p_display_location` | Specifies where the error message is displayed. Use the constants defined for `p_display_location`. See Constants and Attributes Used for Result Types. |
| `p_page_item_name` | Name of the page item on the current page that is highlighted if `apex_error.c_inline_with_field` or `apex_error.c_inline_with_field_and_notif` are used as the display location. |
| `p_ignore_ora_error` | If `FALSE` (default), retains the original error in the error stack. If `TRUE` and `add_error` is called from an exception handler, removes the original error that caused the exception from the error stack. |

---

## ADD_ERROR Procedure Signature 4

This procedure adds an error message to the error stack that is used to display an error for a tabular form inline in a notification. It can be called in a validation or process to add one or more errors to the error stack.

Note:

This procedure must be called before the Oracle APEX application has performed the last validation or process. Otherwise, the error is ignored if it does not have a display location of `apex_error.c_on_error_page`.

Syntax

```sql
APEX_ERROR.ADD_ERROR (
    p_message          IN VARCHAR2,
    p_additional_info  IN VARCHAR2 DEFAULT NULL,
    p_display_location IN VARCHAR2,
    p_region_id        IN NUMBER,
    p_column_alias     IN VARCHAR2 DEFAULT NULL,
    p_row_num          IN NUMBER,
    p_ignore_ora_error IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_message` | Displayed error message. |
| `p_additional_info` | Additional error information needed if the error is displayed on the error page. |
| `p_display_location` | Specifies where the error message is displayed. Use the constant `apex_error.c_inline_with_field` or `apex_error.c_inline_with_field_and_notif`. See Constants and Attributes Used for Result Types. |
| `p_region_id` | The ID of a tabular form region on the current page. The ID can be read from the view `APEX_APPLICATION_PAGE_REGIONS`. |
| `p_column_alias` | Name of a tabular form column alias defined for p_region_id that is highlighted if `apex_error.c_inline_with_field` or `apex_error.c_inline_with_field_and_notif` are used as a display location. |
| `p_row_num` | Number of the tabular form row where the error occurred. |
| `p_ignore_ora_error` | If `FALSE` (default), retains the original error in the error stack. If `TRUE` and `add_error` is called from an exception handler, removes the original error that caused the exception from the error stack. |

---

## ADD_ERROR Procedure Signature 5

Adds an error message to the error stack of a tabular form based on a text message defined in Shared Components. This error message can be displayed in all display locations. It can be called in a validation or process to add one or more errors to the error stack.

Note:

This procedure must be called before the Oracle APEX application has performed the last validation or process. Otherwise, the error is ignored if it does not have a display location of `apex_error.c_on_error_page`.

Syntax

```sql
APEX_ERROR.ADD_ERROR (
    p_error_code          IN VARCHAR2,
    p0                    IN VARCHAR2 DEFAULT NULL,
    p1                    IN VARCHAR2 DEFAULT NULL,
    p2                    IN VARCHAR2 DEFAULT NULL,
    p3                    IN VARCHAR2 DEFAULT NULL,
    p4                    IN VARCHAR2 DEFAULT NULL,
    p5                    IN VARCHAR2 DEFAULT NULL,
    p6                    IN VARCHAR2 DEFAULT NULL,
    p7                    IN VARCHAR2 DEFAULT NULL,
    p8                    IN VARCHAR2 DEFAULT NULL,
    p9                    IN VARCHAR2 DEFAULT NULL,
    p_escape_placeholders IN BOOLEAN  DEFAULT TRUE,
    p_additional_info     IN VARCHAR2 DEFAULT NULL,
    p_display_location    IN VARCHAR2,
    p_region_id           IN NUMBER,
    p_column_alias        IN VARCHAR2 DEFAULT NULL,
    p_row_num             IN NUMBER,
    p_ignore_ora_error    IN BOOLEAN  DEFAULT FALSE );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_error_code` | Name of shared component text message. |
| `p0` through `p9` | Values for %0 through %9 placeholders defined in the text message. |
| `p_escape_placeholders` | If set to `TRUE`, the values provided in `p0` through `p9` are escaped with `sys.htf.escape_sc` before replacing the placeholder in the text message. If set to `FALSE`, values are not escaped. |
| `p_additional_info` | Additional error information needed if the error is displayed on the error page. |
| `p_display_location` | Specifies where the error message is displayed. Use the constants defined for `p_display_location`. See Constants and Attributes Used for Result Types. |
| `p_region_id` | The ID of the tabular form region on the current page. The ID can be read from the view `APEX_APPLICATION_PAGE_REGIONS`. |
| `p_column_alias` | The name of the tabular form column alias defined for `p_region_id` that is highlighted if `apex_error.c_inline_with_field` or `apex_error.c_inline_with_field_and_notif` are used as a display location. |
| `p_row_num` | Number of the tabular form row where the error occurred. |
| `p_ignore_ora_error` | If `FALSE` (default), retains the original error in the error stack. If `TRUE` and `add_error` is called from an exception handler, removes the original error that caused the exception from the error stack. |

---

## AUTO_SET_ASSOCIATED_ITEM Procedure

This procedure automatically sets the associated page item or tabular form column based on a constraint contained in `p_error.ora_sqlerrm`.This procedure performs the following:

* Identifies the constraint by searching for the `schema.constraint` pattern.
* Only supports constraints of type P, U, R and C.
* For constraints of type C (check constraints), the procedure parses the expression to identify those columns that are used in the constraints expression.
* Using those columns, the procedure gets the first visible page item or tabular form column that is based on that column and set it as associated `p_error_result.page_item_name` or `p_error_result.column_alias`.
* If a page item or tabular form column was found, `p_error_result.display_location` is set to `apex_error.c_inline_with_field_and_notif`.

Syntax

```sql
APEX_ERROR.AUTO_SET_ASSOCIATED_ITEM (
    p_error_result IN OUT NOCOPY t_error_result,
    p_error        IN            t_error );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_error_result` | The result variable of your error handling function. |
| `p_error` | The `p_error` parameter of your error handling function. |

---

## EXTRACT_CONSTRAINT_NAME Function

This function extracts a constraint name contained in `p_error.ora_sqlerrm`. The constraint must match the pattern `schema.constraint`.

Syntax

```sql
APEX_ERROR.EXTRACT_CONSTRAINT_NAME (
    p_error          IN t_error,
    p_include_schema IN BOOLEAN DEFAULT FALSE )
    RETURN VARCHAR2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_error` | The `p_error` parameter of your error handling function. |
| `p_include_schema` | If set to `TRUE`, the result is prefixed with the schema name. For example, `HR.DEMO_PRODUCT_INFO_PK`. If set to `FALSE`, only the constraint name is returned. |

---

## GET_FIRST_ORA_ERROR_TEXT Function

This function returns the first ORA error message text stored in `p_error.ora_sqlerrm`. If `p_error_ora_sqlerrm` does not contain a value, `NULL` is returned.

Syntax

```sql
APEX_ERROR.GET_FIRST_ORA_ERROR_TEXT (
    p_error            IN t_error,
    p_include_error_no IN BOOLEAN DEFAULT FALSE )
    RETURN VARCHAR2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_error` | The `p_error` parameter of your error handling function. |
| `p_include_error_no` | If set to `TRUE`, ORA-xxxx is included in the returned error message. If set to `FALSE`, only the error message text is returned. |

---

## HAVE_ERRORS_OCCURRED Function

This function returns `TRUE` if (inline) errors have occurred and `FALSE` if no error has occurred.

Syntax

```sql
APEX_ERROR.HAVE_ERRORS_OCCURRED
RETURN BOOLEAN;
```

---

## INIT_ERROR_RESULT Function

This function returns the t_error_result type initialized with the values stored in `p_error`.

Note:

This function must be used to ensure initialization is compatible with future changes to `t_error_result`.

Syntax

```sql
APEX_ERROR.INIT_ERROR_RESULT (
    p_error  IN t_error)
    RETURN   t_error_result;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_error` | The `p_error` parameter of your error handling function. |