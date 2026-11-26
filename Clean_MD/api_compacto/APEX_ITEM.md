<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_ITEM (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_ITEM (Legacy)

This API is designated as legacy.

You can use the `APEX_ITEM` package to create form elements dynamically based on a SQL query instead of creating individual items page by page.

---

## CHECKBOX2 Function

This function creates check boxes.

Syntax

```sql
APEX_ITEM.CHECKBOX2 (
    p_idx                       IN    NUMBER,
    p_value                     IN    VARCHAR2 DEFAULT NULL,
    p_attributes                IN    VARCHAR2 DEFAULT NULL,
    p_checked_values            IN    VARCHAR2 DEFAULT NULL,
    p_checked_values_delimiter  IN    VARCHAR2 DEFAULT ':',
    p_item_id                   IN    VARCHAR2 DEFAULT NULL,
    p_item_label                IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Number that determines which `APEX_APPLICATION` global variable is used. Valid range of values is 1 to 50. For example 1 creates `F01` and 2 creates `F02` |
| `p_value` | Value of a check box, hidden field, or input form item |
| `p_attributes` | Controls the size of the text field |
| `p_checked_values` | Values to be checked by default |
| `p_checked_values_delimiter` | Delimits the values in the previous parameter, `p_checked_values` |
| `p_item_id` | HTML attribute ID for the `<input>` tag |
| `p_item_label` | Invisible label created for the item |

Examples of Default Check Box Behavior

The following example demonstrates how to create a selected check box for each employee in the `emp` table.

```sql
SELECT APEX_ITEM.CHECKBOX2(1,empno,'CHECKED') "Select",
    ename, job
FROM   emp
ORDER BY 1
```

The following example demonstrates how to have all check boxes for employees display without being selected.

```sql
SELECT APEX_ITEM.CHECKBOX2(1,empno) "Select",
    ename, job
FROM   emp
ORDER BY 1
```

The following example demonstrates how to select the check boxes for employees who work in department 10.

```sql
SELECT APEX_ITEM.CHECKBOX2(1,empno,DECODE(deptno,10,'CHECKED',NULL)) "Select",
    ename, job
FROM   emp
ORDER BY 1
```

The next example demonstrates how to select the check boxes for employees who work in department 10 or department 20.

```sql
SELECT APEX_ITEM.CHECKBOX2(1,deptno,NULL,'10:20',':') "Select",
    ename, job
FROM   emp
ORDER BY 1
```

Creating an On-Submit Process

If you are using check boxes in your application, you might need to create an On Submit process to perform a specific type of action on the selected rows. For example, you could have a Delete button that uses the following logic:

```sql
SELECT APEX_ITEM.CHECKBOX2(1,empno) "Select",
    ename, job
FROM   emp
ORDER  by 1
```

Consider the following sample on-submit process:

```sql
FOR I in 1..APEX_APPLICATION.G_F01.COUNT LOOP
    DELETE FROM emp WHERE empno = to_number(APEX_APPLICATION.G_F01(i));
END LOOP;
```

The following example demonstrates how to create unselected checkboxes for each employee in the emp table, with a unique ID. This is useful for referencing records from within JavaScript code:

```sql
SELECT APEX_ITEM.CHECKBOX2(1,empno,NULL,NULL,NULL,'f01_#ROWNUM#') "Select",
    ename, job
FROM   emp
ORDER BY 1
```

---

## DATE_POPUP Function

Use this function with forms that include date fields. The `DATE_POPUP` function dynamically generates a date field that has a popup calendar button.

Syntax

```sql
APEX_ITEM.DATE_POPUP (
    p_idx                       IN    NUMBER,
    p_row                       IN    NUMBER,
    p_value                     IN    VARCHAR2 DEFAULT NULL,
    p_date_format               IN    DATE DEFAULT 'DD-MON-YYYY',
    p_size                      IN    NUMBER DEFAULT 20,
    p_maxlength                 IN    NUMBER DEFAULT 2000,
    p_attributes                IN    VARCHAR2 DEFAULT NULL,
    p_item_id                   IN    VARCHAR2 DEFAULT NULL,
    p_item_label                IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Number that determines which APEX_APPLICATION global variable is used.Valid range of values is 1 to 50. For example, 1 creates `F01` and 2 creates `F02`. |
| `p_row` | This parameter is deprecated. Anything specified for this value is ignored. |
| `p_value` | Value of a field item. |
| `p_date_format` | Valid database date format. |
| `p_size` | Controls HTML tag attributes (such as disabled). |
| `p_maxlength` | Determines the maximum number of enterable characters. Becomes the maxlength attribute of the `<input>` HTML tag. |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_item_id` | HTML attribute ID for the `<input>` tag. |
| `p_item_label` | Invisible label created for the item. |

---

## DATE_POPUP2 Function

Use this function with forms that include date fields. The DATE_POPUP2 function dynamically generates a date field that has a jQuery based popup calendar with button.

Syntax

```sql
APEX_ITEM.DATE_POPUP2 (
    p_idx                   IN NUMBER,
    p_value                 IN DATE     DEFAULT NULL,
    p_date_format           IN VARCHAR2 DEFAULT NULL,
    p_size                  IN NUMBER   DEFAULT 20,
    p_maxLength             IN NUMBER   DEFAULT 2000,
    p_attributes            IN VARCHAR2 DEFAULT NULL,
    p_item_id               IN VARCHAR2 DEFAULT NULL,
    p_item_label            IN VARCHAR2 DEFAULT NULL,
    p_default_value         IN VARCHAR2 DEFAULT NULL,
    p_max_value             IN VARCHAR2 DEFAULT NULL,
    p_min_value             IN VARCHAR2 DEFAULT NULL,
    p_show_on               IN VARCHAR2 DEFAULT 'button',
    p_number_of_months      IN VARCHAR2 DEFAULT NULL,
    p_navigation_list_for   IN VARCHAR2 DEFAULT 'none',
    p_year_range            IN VARCHAR2 DEFAULT NULL,
    p_validation_date       IN VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Number that determines which APEX_APPLICATION global variable is used. Valid range of values is 1 to 50. For example, 1 creates F01 and 2 creates F02. |
| `p_value` | Value of a field item. |
| `p_date_format` | Valid database date format. |
| `p_size` | Controls HTML tag attributes (such as disabled). |
| `p_maxlength` | Determines the maximum number of enterable characters. Becomes the maxlength attribute of the `<input>` HTML tag. |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_item_id` | HTML attribute ID for the `<input>` tag. |
| `p_item_label` | Invisible label created for the item. |
| `p_default_value` | The default date which should be selected in datepicker calendar popup. |
| `p_max_value` | The Maximum date that can be selected from the datepicker. |
| `p_min_value` | The Minimum date that can be selected from the datepicker. |
| `p_show_on` | Determines when the datepicker displays, on button click or on focus of the item or both. |
| `p_number_of_months` | Determines number of months displayed. Value should be in this array format: `[row,column]` |
| `p_navigation_list_for` | Determines if a select list is displayed for Changing Month, Year, or Both. Possible values include: `MONTH`, `YEAR`, `MONTH_AND_YEAR`. Default NULL. |
| `p_year_range` | The range of years displayed in the year selection list. |
| `p_validation_date` | Used to store the Date value for the which date validation failed. |

See Also:

Oracle Database SQL
Language Reference for information about the `TO_CHAR` or `TO_DATE` functions

---

## DISPLAY_AND_SAVE Function

Use this function to display an item as text, but save its value to session state.

Syntax

```sql
APEX_ITEM.DISPLAY_AND_SAVE (
    p_idx         IN    NUMBER,
    p_value       IN    VARCHAR2 DEFAULT NULL,
    p_item_id     IN    VARCHAR2 DEFAULT NULL,
    p_item_label  IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Number that determines which `APEX_APPLICATION` global variable is used.Valid range of values is 1 to 50. For example, 1 creates `F01` and 2 creates `F02`. |
| `p_value` | Current value. |
| `p_item_id` | HTML attribute ID for the `<span>` tag. |
| `p_item_label` | Invisible label created for the item. |

---

## HIDDEN Function

This function dynamically generates hidden form items.

Syntax

```sql
APEX_ITEM.HIDDEN (
    p_idx         IN    NUMBER,
    p_value       IN    VARCHAR2 DEFAULT
    p_attributes  IN    VARCHAR2 DEFAULT NULL,
    p_item_id     IN    VARCHAR2 DEFAULT NULL,
    p_item_label  IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Number to identify the item you want to generate. The number determines which `G_FXX` global is populated  See also APEX_APPLICATION. |
| `p_value` | Value of the hidden input form item. |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_item_id` | HTML attribute ID for the `<input>` tag. |
| `p_item_label` | Invisible label created for the item. |

---

## MD5_CHECKSUM Function

Use this function for lost update detection. Lost update detection ensures data integrity in applications where data can be accessed concurrently.

This function produces hidden form fields with a name attribute equal to `fcs` and as value a MD5 checksum based on up to 50 inputs. APEX_ITEM.MD5_CHECKSUM also produces an MD5 checksum using Oracle Database DBMS_CRYPTO:

```sql
DBMS_CRYPTO.HASH (
    SRC => UTL_RAW.CAST_TO_RAW('my_string'),
    TYP => DBMS_CRYPTO.HASH_MD5 );
```

An MD5 checksum provides data integrity through hashing and sequencing to ensure that data is not altered or stolen as it is transmitted over a network.

Syntax

```sql
APEX_ITEM.MD5_CHECKSUM (
    p_value01   IN    VARCHAR2 DEFAULT NULL,
    p_value02   IN    VARCHAR2 DEFAULT NULL,
    p_value03   IN    VARCHAR2 DEFAULT NULL,
    ...
    p_value50   IN    VARCHAR2 DEFAULT NULL,
    p_col_sep   IN    VARCHAR2 DEFAULT '|',
    p_item_id   IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value01`  `...`  `p_value50` | Fifty available inputs. If no parameters are supplied, defaults to NULL. |
| `p_col_sep` | String used to separate `p_value` inputs. Defaults to | (pipe symbol). |
| `p_item_id` | ID of the HTML form item. |

---

## MD5_HIDDEN Function

Use this function for lost update detection. Lost update detection ensures data integrity in applications where data can be accessed concurrently.

This function produces a hidden form field with a MD5 checksum as value which is based on up to 50 inputs. `APEX_ITEM`.`MD5_HIDDEN` also produces an MD5 checksum using Oracle database `DBMS_CRYPTO`:

```sql
UTL_RAW.CAST_TO_RAW(DBMS_CRYPTO.MD5())
```

An MD5 checksum provides data integrity through hashing and sequencing to ensure that data is not altered or stolen as it is transmitted over a network.

Syntax

```sql
APEX_ITEM.MD5_HIDDEN (
    p_idx       IN    NUMBER,
    p_value01   IN    VARCHAR2 DEFAULT NULL,
    p_value02   IN    VARCHAR2 DEFAULT NULL,
    p_value03   IN    VARCHAR2 DEFAULT NULL,
    ...
    p_value50   IN    VARCHAR2 DEFAULT NULL,
    p_col_sep   IN    VARCHAR2 DEFAULT '|',
    p_item_id   IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Indicates the form element to be generated. For example, 1 equals `F01` and 2 equals `F02`. Typically the `p_idx` parameter is constant for a given column. |
| `p_value01...50` | Fifty available inputs. Parameters not supplied default to NULL. |
| `p_col_sep` | String used to separate `p_value` inputs. Defaults to the pipe symbol ( | ). |
| `p_item_id` | ID of the HTML form item. |

---

## POPUP_FROM_LOV Function

This function generates an HTML popup select list from an application shared list of values (LOV). Like other available functions in the `APEX_ITEM` package, `POPUP_FROM_LOV` function is designed to generate forms with `F01` to `F50` form array elements.

Syntax

```sql
APEX_ITEM.POPUP_FROM_LOV (
    p_idx              IN    NUMBER,
    p_value            IN    VARCHAR2 DEFAULT NULL,
    p_lov_name         IN    VARCHAR2,
    p_width            IN    VARCHAR2 DEFAULT NULL,
    p_max_length       IN    VARCHAR2 DEFAULT NULL,
    p_form_index       IN    VARCHAR2 DEFAULT '0',
    p_escape_html      IN    VARCHAR2 DEFAULT NULL,
    p_max_elements     IN    VARCHAR2 DEFAULT NULL,
    p_attributes       IN    VARCHAR2 DEFAULT NULL,
    p_ok_to_query      IN    VARCHAR2 DEFAULT 'YES',
    p_item_id          IN    VARCHAR2 DEFAULT NULL,
    p_item_label       IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Form element name. For example, `1` equals `F01` and `2` equals `F02`. Typically, `p_idx` is a constant for a given column. |
| `p_value` | Form element current value. This value should be one of the values in the `p_lov_name` parameter. |
| `p_lov_name` | Named LOV used for this popup. |
| `p_width` | Width of the text box. |
| `p_max_length` | Maximum number of characters that can be entered in the text box. |
| `p_form_index` | HTML form on the page in which an item is contained. Defaults to 0 (rarely used).  Only use this parameter when it is necessary to embed a custom form in your page template (such as a search field that posts to a different website). If this form comes before the `#FORM_OPEN#` substitution string, then its index is zero and the form opened automatically by Oracle APEX must be referenced as form 1. This functionality supports the JavaScript used in the popup LOV that passes a value back to a form element. |
| `p_escape_html` | Replacements for special characters that require an escaped equivalent:   * `&lt;` for `<` * `&gt;` for `>` * `&amp;` for `&`   Range of values is `YES` and `NO`. If `YES`, special characters are escaped. This parameter is useful if you know your query returns invalid HTML. |
| `p_max_elements` | Limit on the number of rows that can be returned by your query. Limits the performance impact of user searches. By entering a value in this parameter, you force the user to search for a narrower set of results. |
| `p_attributes` | Additional HTML attributes to use for the form item. |
| `p_ok_to_query` | Range of values is `YES` and `NO`. If `YES`, a popup returns first set of rows for the LOV. If `NO`, a search is initiated to return rows. |
| `p_item_id` | ID attribute of the form element. |
| `p_item_label` | Invisible label created for the item. |

---

## POPUP_FROM_QUERY Function

Generates an HTML popup select list from a query. This function is designed to generate forms with `F01` to `F50` form array elements.

Syntax

```sql
APEX_ITEM.POPUP_FROM_QUERY (
    p_idx              IN    NUMBER,
    p_value            IN    VARCHAR2 DEFAULT NULL,
    p_lov_query        IN    VARCHAR2,
    p_width            IN    VARCHAR2 DEFAULT NULL,
    p_max_length       IN    VARCHAR2 DEFAULT NULL,
    p_form_index       IN    VARCHAR2 DEFAULT '0',
    p_escape_html      IN    VARCHAR2 DEFAULT NULL,
    p_max_elements     IN    VARCHAR2 DEFAULT NULL,
    p_attributes       IN    VARCHAR2 DEFAULT NULL,
    p_ok_to_query      IN    VARCHAR2 DEFAULT 'YES',
    p_item_id          IN    VARCHAR2 DEFAULT NULL,
    p_item_label       IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Form element name. For example, `1` equals `F01` and `2` equals `F02`. Typically, `p_idx` is a constant for a given column. |
| `p_value` | Form element current value. This value should be one of the values in the `p_lov_query` parameter. |
| `p_lov_query` | SQL query that is expected to select two columns (a display column and a return column). For example:   ```sql SELECT dname, deptno FROM dept ``` |
| `p_width` | Width of the text box. |
| `p_max_length` | Maximum number of characters that can be entered in the text box. |
| `p_form_index` | HTML form on the page in which an item is contained. Defaults to 0 and rarely used.  Only use this parameter when it is necessary to embed a custom form in your page template (such as a search field that posts to a different website). If this form comes before the `#FORM_OPEN#` substitution string, then its index is zero and the form opened automatically by Oracle APEX must be referenced as form 1. This functionality supports the JavaScript used in the popup LOV that passes a value back to a form element. |
| `p_escape_html` | Replacements for special characters that require an escaped equivalent.   * `&lt;` for `<` * `&gt;` for `>` * `&amp;` for `&`   Range of values is `YES` and `NO`. If `YES`, special characters are escaped. This parameter is useful if you know your query returns invalid HTML. |
| `p_max_elements` | Limit on the number of rows that can be returned by your query. Limits the performance impact of user searches. By entering a value in this parameter, you force the user to search for a narrower set of results. |
| `p_attributes` | Additional HTML attributes to use for the form item. |
| `p_ok_to_query` | Range of values is `YES` and `NO`. If `YES`, a popup returns the first set of rows for the LOV. If `NO`, a search is initiated to return rows. |
| `p_item_id` | ID attribute of the form element. |
| `p_item_label` | Invisible label created for the item. |

---

## POPUPKEY_FROM_LOV Function

This function generates a popup key select list from a shared list of values (LOV). Similar to other available functions in the `APEX_ITEM` package, the `POPUPKEY_FROM_LOV` function is designed to generate forms with `F01` to `F50` form array elements.

Syntax

```sql
APEX_ITEM.POPUPKEY_FROM_LOV (
    p_idx              IN    NUMBER,
    p_value            IN    VARCHAR2 DEFAULT NULL,
    p_lov_name         IN    VARCHAR2,
    p_width            IN    VARCHAR2 DEFAULT NULL,
    p_max_length       IN    VARCHAR2 DEFAULT NULL,
    p_form_index       IN    VARCHAR2 DEFAULT '0',
    p_escape_html      IN    VARCHAR2 DEFAULT NULL,
    p_max_elements     IN    VARCHAR2 DEFAULT NULL,
    p_attributes       IN    VARCHAR2 DEFAULT NULL,
    p_ok_to_query      IN    VARCHAR2 DEFAULT 'YES',
    p_item_id          IN    VARCHAR2 DEFAULT NULL,
    p_item_label       IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Although the text field associated with the popup displays in the first column in the LOV query, the actual value is specified in the second column in the query.

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Identifies a form element name. For example, `1` equals `F01` and `2` equals `F02`. Typically, `p_idx` is a constant for a given column  Because of the behavior of `POPUPKEY_FROM_QUERY`, the next index value should be `p_idx + 1`. For example:   ```sql SELECT APEX_ITEM.POPUPKEY_FROM_LOV (1,deptno,'DEPT') dt,     APEX_ITEM.HIDDEN(3,empno) eno     FROM emp; ``` |
| `p_value` | Indicates the current value. This value should be one of the values in the `P_LOV_NAME` parameter. |
| `p_lov_name` | Identifies a named LOV used for this popup. |
| `p_width` | Width of the text box. |
| `p_max_length` | Maximum number of characters that can be entered in the text box. |
| `p_form_index` | HTML form on the page in which an item is contained. Defaults to 0 and rarely used.  Only use this parameter when it is necessary to embed a custom form in your page template (such as a search field that posts to a different website). If this form comes before the `#FORM_OPEN#` substitution string, then its index is zero and the form opened automatically by APEX must be referenced as form 1. This functionality supports the JavaScript used in the popup LOV that passes a value back to a form element. |
| `p_escape_html` | Replacements for special characters that require an escaped equivalent.   * `&lt;` for `<` * `&gt;` for `>` * `&amp;` for `&`   This parameter is useful if you know your query returns invalid HTML. |
| `p_max_elements` | Limit on the number of rows that can be returned by your query. Limits the performance impact of user searches. By entering a value in this parameter, you force the user to search for a narrower set of results. |
| `p_attributes` | Additional HTML attributes to use for the form item. |
| `p_ok_to_query` | Range of values is `YES` and `NO`. If `YES`, a popup returns the first set of rows for the LOV. If `NO`, a search is initiated to return rows. |
| `p_item_id` | HTML attribute ID for the <input> tag. |
| `p_item_label` | Invisible label created for the item. |

---

## POPUPKEY_FROM_QUERY Function

This function generates a popup key select list from a SQL query. Similar to other available functions in the `APEX_ITEM` package, the `POPUPKEY_FROM_QUERY` function is designed to generate forms with `F01` to `F50` form array elements.

Syntax

```sql
APEX_ITEM.POPUPKEY_FROM_QUERY (
    p_idx              IN    NUMBER,
    p_value            IN    VARCHAR2 DEFAULT NULL,
    p_lov_query        IN    VARCHAR2,
    p_width            IN    VARCHAR2 DEFAULT NULL,
    p_max_length       IN    VARCHAR2 DEFAULT NULL,
    p_form_index       IN    VARCHAR2 DEFAULT '0',
    p_escape_html      IN    VARCHAR2 DEFAULT NULL,
    p_max_elements     IN    VARCHAR2 DEFAULT NULL,
    p_attributes       IN    VARCHAR2 DEFAULT NULL,
    p_ok_to_query      IN    VARCHAR2 DEFAULT 'YES',
    p_item_id          IN    VARCHAR2 DEFAULT NULL,
    p_item_label       IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Form element name. For example, `1` equals `F01` and `2` equals `F02`. Typically, `p_idx` is a constant for a given column.  Because of the behavior of `POPUPKEY_FROM_QUERY`, the next index value should be `p_idx + 1`. For example:   ```sql SELECT APEX_ITEM.POPUPKEY_FROM_QUERY (1,deptno,'SELECT dname, deptno FROM dept') dt, APEX_ITEM.HIDDEN(3,empno) eno ``` |
| `p_value` | Form element current value. This value should be one of the values in the `P_LOV_QUERY` parameter. |
| `p_lov_query` | LOV query used for this popup. |
| `p_width` | Width of the text box. |
| `p_max_length` | Maximum number of characters that can be entered in the text box. |
| `p_form_index` | HTML form on the page in which an item is contained. Defaults to 0 and rarely used.  Only use this parameter when it is necessary to embed a custom form in your page template (such as a search field that posts to a different website). If this form comes before the `#FORM_OPEN#` substitution string, then its index is zero and the form opened automatically by Oracle APEX must be referenced as form 1. This functionality supports the JavaScript used in the popup LOV that passes a value back to a form element. |
| `p_escape_html` | Replacements for special characters that require an escaped equivalent.   * `&lt;` for `<` * `&gt;` for `>` * `&amp;` for `&`   This parameter is useful if you know your query returns illegal HTML. |
| `p_max_elements` | Limit on the number of rows that can be returned by your query. Limits the performance impact of user searches. By entering a value in this parameter, you force the user to search for a narrower set of results. |
| `p_attributes` | Additional HTML attributes to use for the form item. |
| `p_ok_to_query` | Range of values is `YES` and `NO`. If `YES`, a popup returns first set of rows for the LOV. If `NO`, a search is initiated to return rows. |
| `p_item_id` | ID attribute of the form element. |
| `p_item_label` | Invisible label created for the item. |

---

## RADIOGROUP Function

This function generates a radio group from a SQL query.

Syntax

```sql
APEX_ITEM.RADIOGROUP (
    p_idx              IN    NUMBER,
    p_value            IN    VARCHAR2 DEFAULT NULL,
    p_selected_value   IN    VARCHAR2 DEFAULT NULL,
    p_display          IN    VARCHAR2 DEFAULT NULL,
    p_attributes       IN    VARCHAR2 DEFAULT NULL,
    p_onblur           IN    VARCHAR2 DEFAULT NULL,
    p_onchange         IN    VARCHAR2 DEFAULT NULL,
    p_onfocus          IN    VARCHAR2 DEFAULT NULL,
    p_item_id          IN    VARCHAR2 DEFAULT NULL,
    p_item_label       IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Number that determines which `APEX_APPLICATION` global variable is used. Valid range of values is `1` to `50`.For example `1` creates `F01` and `2` creates `F02`. |
| `p_value` | Value of the radio group. |
| `p_selected_value` | Value that should be selected. |
| `p_display` | Text to display next to the radio option. |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_onblur` | JavaScript to execute in the `onBlur` event. |
| `p_onchange` | JavaScript to execute in the `onChange` event. |
| `p_onfocus` | JavaScript to execute in the `onFocus` event. |
| `p_item_id` | HTML attribute ID for the <input> tag. |
| `p_item_label` | Invisible label created for the item. |

---

## SELECT_LIST Function

This function dynamically generates a static select list. This function is designed to generate forms with `F01` to `F50` form array elements.

Syntax

```sql
APEX_ITEM.SELECT_LIST (
    p_idx           IN   NUMBER,
    p_value         IN   VARCHAR2 DEFAULT NULL,
    p_list_values   IN   VARCHAR2 DEFAULT NULL,
    p_attributes    IN   VARCHAR2 DEFAULT NULL,
    p_show_null     IN   VARCHAR2 DEFAULT 'NO',
    p_null_value    IN   VARCHAR2 DEFAULT '%NULL%',
    p_null_text     IN   VARCHAR2 DEFAULT '%',
    p_item_id       IN   VARCHAR2 DEFAULT NULL,
    p_item_label    IN   VARCHAR2 DEFAULT NULL,
    p_show_extra    IN   VARCHAR2 DEFAULT 'YES' )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Form element name. For example, `1` equals `F01` and `2` equals `F02`. Typically the `P_IDX` parameter is constant for a given column. |
| `p_value` | Current value. This value should be a value in the `P_LIST_VALUES` parameter. |
| `p_list_values` | List of static values separated by commas. Displays values and returns values that are separated by semicolons.  Note that this is only available in the `SELECT_LIST` function. |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_show_null` | Extra select option to enable the NULL selection. Range of values is `YES` and `NO`. |
| `p_null_value` | Value to be returned when a user selects the NULL option. Only relevant when `p_show_null` equals `YES`. |
| `p_null_text` | Value to be displayed when a user selects the NULL option. Only relevant when `p_show_null` equals `YES`. |
| `p_item_id` | HTML attribute ID for the <`input`> tag. |
| `p_item_label` | Invisible label created for the item. |
| `p_show_extra` | Shows the current value even if the value of p_value is not located in the select list. |

---

## SELECT_LIST_FROM_LOV Function

This function dynamically generates select lists from a shared list of values (LOV). Similar to other functions available in the `APEX_ITEM` package, these select list functions are designed to generate forms with `F01` to `F50` form array elements.

This function is the same as `SELECT_LIST_FROM_LOV_XL`, but its return value is `VARCHAR2`. Returned values are limited to 32k.

Syntax

```sql
APEX_ITEM.SELECT_LIST_FROM_LOV (
    p_idx           IN   NUMBER,
    p_value         IN   VARCHAR2 DEFAULT NULL,
    p_lov           IN   VARCHAR2,
    p_attributes    IN   VARCHAR2 DEFAULT NULL,
    p_show_null     IN   VARCHAR2 DEFAULT 'YES',
    p_null_value    IN   VARCHAR2 DEFAULT '%NULL%',
    p_null_text     IN   VARCHAR2 DEFAULT '%',
    p_item_id       IN   VARCHAR2 DEFAULT NULL,
    p_item_label    IN   VARCHAR2 DEFAULT NULL,
    p_show_extra    IN   VARCHAR2 DEFAULT 'YES' )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Form element name. For example, `1` equals `F01` and `2` equals `F02`. Typically, the `p_idx` parameter is constant for a given column. |
| `p_value` | Current value. This value should be a value in the `p_lov` parameter. |
| `p_lov` | Text name of an application list of values. This list of values must be defined in your application. This parameter is used only by the `select_list_from_lov` function. |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_show_null` | Extra select option to enable the NULL selection. Range of values is `YES` and `NO`. |
| `p_null_value` | Value to be returned when a user selects the NULL option. Only relevant when `p_show_null` equals `YES`. |
| `p_null_text` | Value to be displayed when a user selects the NULL option. Only relevant when `p_show_null` equals `YES`. |
| `p_item_id` | HTML attribute ID for the `<select>` tag. |
| `p_item_label` | Invisible label created for the item. |
| `p_show_extra` | Shows the current value even if the value of `p_value` is not located in the select list. |

---

## SELECT_LIST_FROM_LOV_XL Function

This function dynamically generates very large select lists (greater than 32K) from a shared list of values (LOV). Use this function in SQL queries where you need to handle a column value longer than 4000 characters.

Similar to other functions available in the `APEX_ITEM` package, these select list functions are designed to generate forms with `F01` to `F50` form array elements.

This function is the same as `SELECT_LIST_FROM_LOV`, but its return value is CLOB.

Syntax

```sql
APEX_ITEM.SELECT_LIST_FROM_LOV_XL (
    p_idx           IN   NUMBER,
    p_value         IN   VARCHAR2 DEFAULT NULL,
    p_lov           IN   VARCHAR2,
    p_attributes    IN   VARCHAR2 DEFAULT NULL,
    p_show_null     IN   VARCHAR2 DEFAULT 'YES',
    p_null_value    IN   VARCHAR2 DEFAULT '%NULL%',
    p_null_text     IN   VARCHAR2 DEFAULT '%',
    p_item_id       IN   VARCHAR2 DEFAULT NULL,
    p_item_label    IN   VARCHAR2 DEFAULT NULL,
    p_show_extra    IN   VARCHAR2 DEFAULT 'YES' )
    RETURN CLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Form element name. For example, `1` equals `F01` and `2` equals `F02`. Typically, the `p_idx` parameter is constant for a given column. |
| `p_value` | Current value. This value should be a value in the `p_lov` parameter. |
| `p_lov` | Text name of a list of values. This list of values must be defined in your application. This parameter is used only by the `select_list_from_lov` function. |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_show_null` | Extra select option to enable the NULL selection. Range of values is `YES` and `NO`. |
| `p_null_value` | Value to be returned when a user selects the NULL option. Only relevant when `p_show_null` equals `YES`. |
| `p_null_text` | Value to be displayed when a user selects the NULL option. Only relevant when `p_show_null` equals `YES`. |
| `p_item_id` | HTML attribute ID for the `<select>` tag. |
| `p_item_label` | Invisible label created for the item. |
| `p_show_extra` | Shows the current value even if the value of `p_value` is not located in the select list. |

---

## SELECT_LIST_FROM_QUERY Function

This function dynamically generates a select list from a query. Similar to other functions available in the `APEX_ITEM` package, these select list functions are designed to generate forms with `F01` to `F50` form array elements.

Syntax

```sql
APEX_ITEM.SELECT_LIST_FROM_QUERY (
    p_idx           IN    NUMBER,
    p_value         IN    VARCHAR2 DEFAULT NULL,
    p_query         IN    VARCHAR2,
    p_attributes    IN    VARCHAR2 DEFAULT NULL,
    p_show_null     IN    VARCHAR2 DEFAULT 'YES',
    p_null_value    IN    VARCHAR2 DEFAULT '%NULL%',
    p_null_text     IN    VARCHAR2 DEFAULT '%',
    p_item_id       IN    VARCHAR2 DEFAULT NULL,
    p_item_label    IN    VARCHAR2 DEFAULT NULL,
    p_show_extra    IN    VARCHAR2 DEFAULT 'YES' )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Form element name. For example, `1` equals `F01` and `2` equals `F02`. Typically, the `p_idx` parameter is constant for a given column. |
| `p_value` | Current value. This value should be a value in the `p_query` parameter. |
| `p_query` | SQL query that is expected to select two columns, a display column, and a return column. For example:   ```sql SELECT dname, deptno FROM dept ```   Note that this is used only by the `SELECT_LIST_FROM_QUERY` function.  Also note, if only one column is specified in the select clause of this query, the value for this column is used for both display and return purposes. |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_show_null` | Extra select option to enable the NULL selection. Range of values is `YES` and `NO`. |
| `p_null_value` | Value to be returned when a user selects the NULL option. Only relevant when `p_show_null` equals `YES`. |
| `p_null_text` | Value to be displayed when a user selects the NULL option. Only relevant when `p_show_null` equals `YES`. |
| `p_item_id` | HTML attribute ID for the `<select>` tag. |
| `p_item_label` | Invisible label created for the item. |
| `p_show_extra` | Show the current value even if the value of `p_value` is not located in the select list. |

---

## SELECT_LIST_FROM_QUERY_XL Function

This function is the same as `SELECT_LIST_FROM_QUERY`, but its return value is a CLOB. This allows its use in SQL queries where you need to handle a column value longer than 4000 characters. Returned values will be limited to 32K. Similar to other functions available in the `APEX_ITEM` package, these select list functions are designed to generate forms with `F01` to `F50` form array elements.

Syntax

```sql
APEX_ITEM.SELECT_LIST_FROM_QUERY_XL (
    p_idx           IN    NUMBER,
    p_value         IN    VARCHAR2 DEFAULT NULL,
    p_query         IN    VARCHAR2,
    p_attributes    IN    VARCHAR2 DEFAULT NULL,
    p_show_null     IN    VARCHAR2 DEFAULT 'YES',
    p_null_value    IN    VARCHAR2 DEFAULT '%NULL%',
    p_null_text     IN    VARCHAR2 DEFAULT '%',
    p_item_id       IN    VARCHAR2 DEFAULT NULL,
    p_item_label    IN    VARCHAR2 DEFAULT NULL,
    p_show_extra    IN    VARCHAR2 DEFAULT 'YES' )
    RETURN CLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Form element name. For example, `1` equals `F01` and `2` equals `F02`. Typically the `p_idx` parameter is constant for a given column. |
| `p_value` | Current value. This value should be a value in the `p_query` parameter. |
| `p_query` | SQL query that is expected to select two columns, a display column, and a return column. For example:   ```sql SELECT dname, deptno FROM dept ```   Note that this is used only by the `SELECT_LIST_FROM_QUERY_XL` function.  Also note, if only one column is specified in the select clause of this query, the value for this column is used for both display and return purposes. |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_show_null` | Extra select option to enable the NULL selection. Range of values is `YES` and `NO`. |
| `p_null_value` | Value to be returned when a user selects the NULL option. Only relevant when `p_show_null` equals `YES`. |
| `p_null_text` | Value to be displayed when a user selects the NULL option. Only relevant when `p_show_null` equals `YES`. |
| `p_item_id` | HTML attribute ID for the `<select>` tag. |
| `p_item_label` | Invisible label created for the item. |
| `p_show_extra` | Show the current value even if the value of `p_value` is not located in the select list. |

---

## SWITCH Function

This function dynamically generates flip toggle item. If On/Off value and label are not passed, it renders Yes/No toggle. This function is designed to generate forms with F01 to F50 form array elements.

Syntax

```sql
APEX_ITEM.SWITCH (
    p_idx           IN NUMBER,
    p_value         IN VARCHAR2,
    p_on_value      IN VARCHAR2 DEFAULT 'Y',
    p_on_label      IN VARCHAR2 DEFAULT 'Yes',
    p_off_value     IN VARCHAR2 DEFAULT 'N',
    p_off_label     IN VARCHAR2 DEFAULT 'No',
    p_item_id       IN VARCHAR2 DEFAULT NULL,
    p_item_label    IN VARCHAR2,
    p_attributes    IN VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Form element name. For example, 1 equals F01 and 2 equals F02. Typically the `P_IDX` parameter is constant for a given column. |
| `p_value` | Form element current value. |
| `p_on_value` | The value of the item if the user picks On option. |
| `p_on_label` | The display text for the On option. |
| `p_off_value` | The value of the item if the user picks Off option. |
| `p_off_label` | The display text for the Off option. |
| `p_item_id` | HTML attribute ID for the <input> tag. Try concatenating some string with rownum to make it unique. |
| `p_item_label` | Invisible label created for the item. |
| `p_attributes` | Additional HTML attributes to use for the form item. |

---

## TEXT Function

This function generates text fields (or text input form items) from a SQL query.

Syntax

```sql
APEX_ITEM.TEXT(
    p_idx         IN    NUMBER,
    p_value       IN    VARCHAR2 DEFAULT NULL,
    p_size        IN    NUMBER   DEFAULT NULL,
    p_maxlength   IN    NUMBER   DEFAULT NULL,
    p_attributes  IN    VARCHAR2 DEFAULT NULL,
    p_item_id     IN    VARCHAR2 DEFAULT NULL,
    p_item_label  IN    VARCHAR2 DEFAULT NULL)
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Number to identify the item you want to generate. The number determines which `G_FXX` global is populated.  See also APEX_APPLICATION. |
| `p_value` | Value of a text field item. |
| `p_size` | Controls HTML tag attributes (such as disabled). |
| `p_maxlength` | Maximum number of characters that can be entered in the text box. |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_item_id` | HTML attribute ID for the `<input>` tag. |
| `p_item_label` | Invisible label created for the item. |

---

## TEXTAREA Function

This function creates text areas.

Syntax

```sql
APEX_ITEM.TEXTAREA (
    p_idx         IN    NUMBER,
    p_value       IN    VARCHAR2 DEFAULT NULL,
    p_rows        IN    NUMBER   DEFAULT 40,
    p_cols        IN    NUMBER   DEFAULT 4,
    p_attributes  IN    VARCHAR2 DEFAULT NULL,
    p_item_id     IN    VARCHAR2 DEFAULT NULL,
    p_item_label  IN    VARCHAR2 DEFAULT NULL )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_idx` | Number to identify the item you want to generate. The number determines which `G_FXX` global is populated.  See also APEX_APPLICATION. |
| `p_value` | Value of the text area item. |
| `p_rows` | Height of the text area (HTML rows attribute). |
| `p_cols` | Width of the text area (HTML column attribute). |
| `p_attributes` | Extra HTML parameters you want to add. |
| `p_item_id` | HTML attribute ID for the `<textarea>` tag. |
| `p_item_label` | Invisible label created for the item. |

---

## TEXT_FROM_LOV Function

Displays an item as text, deriving the display value of the named LOV.

Syntax

```sql
APEX_ITEM.TEXT_FROM_LOV (
    p_value       IN    VARCHAR2 DEFAULT NULL,
    p_lov         IN    VARCHAR2,
    p_null_text   IN    VARCHAR2 DEFAULT '%' )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | Value of a field item.  Note that if `p_value` is not located in the list of values, `p_null_text` is displayed. |
| `p_lov` | Text name of a shared list of values. This list of values must be defined in your application. |
| `p_null_text` | Value displayed when the value of the field item is NULL. |

---

## TEXT_FROM_LOV_QUERY Function

Display an item as text, deriving the display value from a list of values query.

Syntax

```sql
APEX_ITEM.TEXT_FROM_LOV_QUERY (
    p_value       IN    VARCHAR2 DEFAULT NULL,
    p_query       IN    VARCHAR2,
    p_null_text   IN    VARCHAR2 DEFAULT '%' )
    RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_value` | Value of a field item. |
| `p_query` | SQL query that is expected to select two columns, a display column and a return column. For example:   ```sql SELECT dname, deptno FROM dept ```   Note if only one column is specified in the select clause of this query, the value for this column is used for both display and return purposes. |
| `p_null_text` | Value to be displayed when the value of the field item is NULL or a corresponding entry is not located for the value `p_value` in the list of values query. |