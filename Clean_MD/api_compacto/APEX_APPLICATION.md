<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_APPLICATION (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_APPLICATION

The `APEX_APPLICATION` package is a PL/SQL package that implements the Oracle APEX rendering engine. You can use this package to take advantage of many global variables.

---

## Working with G_Fnn Arrays (Legacy)

Important:

Support for G_Fnn arrays is legacy and will be removed in a future release. Oracle recommends using interactive grids instead.

The `APEX_APPLICATION.G_Fnn` arrays (where nn ranges from `01` to `50`) are used with `APEX_ITEM` functions to enable the dynamic generation of HTML form elements to an APEX page (such as `APEX_ITEM.TEXT` and `APEX_ITEM.SELECT_LIST`). On Page Submit, the item values are sent to the server and provided as the `APEX_APPLICATION.G_Fnn` arrays.

Only use `APEX_APPLICATION.G_Fnn` in an `APEX_ITEM` context. For other contexts (such as plain array processing for PL/SQL code) use the `APEX_T_VARCHAR2` type and the procedures and functions within the `APEX_STRING` package.

Note:

When working with `APEX_APPLICATION.G_Fnn`, the `TABLE_TO_STRING` and `STRING_TO_TABLE` functions in `APEX_UTIL` are deprecated. Use `APEX_STRING.TABLE_TO_STRING` and `APEX_STRING.STRING_TO_TABLE` instead.

Referencing G_Fnn Arrays

The following example uses `APEX_ITEM` to manually create a tabular form on the `EMP` table. Note that the `ename`, `sal`, and `comm` columns use the `APEX_ITEM.TEXT` function to generate an HTML text field for each row. Note also that each item in the query is passed a unique `p_idx` parameter to ensure that each column is stored in its own array.

1. On a new page, add a classic report with a SQL Query such as the following example:

   ```sql
   SELECT
     empno,
     APEX_ITEM.HIDDEN(1,empno)||
     APEX_ITEM.TEXT(2,ename) ename,
     APEX_ITEM.TEXT(3,job) job,
     mgr,
     APEX_ITEM.DATE_POPUP(4,rownum,hiredate,'dd-mon-yyyy') hiredate,
     APEX_ITEM.TEXT(5,sal) sal,
     APEX_ITEM.TEXT(6,comm) comm,
     deptno
   FROM emp
   ORDER BY 1
   ```
2. Disable "Escape Special Characters" for all report columns (under the Security property in Page Designer).
3. Add a Submit button to the page.
4. Run the application.

Referencing Values Within an On Submit Process

You can reference the values posted by the tabular form using the PL/SQL variable `APEX_APPLICATION.G_F01` to `APEX_APPLICATION.G_F50`. Because this element is an array, you can reference values directly. For example, the following code block collects all employee names as a text block and stores it as the value of the `P3_G_F01_CONTENTS` item:

```sql
:P3_G_F01_CONTENTS := '';
for i IN 1..APEX_APPLICATION.G_F01.COUNT LOOP
    :P3_G_F01_CONTENTS := :P3_G_F01_CONTENTS
                       || 'element '||I||' has a value of '||APEX_APPLICATION.G_F02(i) || chr(10);
END LOOP;
```

Note that check boxes displayed using `APEX_ITEM.CHECKBOX` only contain values in the `APEX_APPLICATION` arrays for those rows which are checked. Unlike other items (`TEXT`, `TEXTAREA`, and `DATE_POPUP`) which can contain an entry in the corresponding `APEX_APPLICATION` array for every row submitted, a check box only has an entry in the `APEX_APPLICATION` array if it is selected.

See Also:

* APEX_IG
* APEX_ITEM (Legacy)
* APEX_STRING
* STRING_TO_TABLE Function
* TABLE_TO_STRING Function

---

## Global Variables

| Global Variable | Description |
| --- | --- |
| `G_USER` | Specifies the currently logged in user. |
| `G_FLOW_ID` | Specifies the ID of the currently running application. |
| `G_FLOW_STEP_ID` | Specifies the ID of the currently running page. |
| `G_FLOW_OWNER` | Defaults to the application's parsing schema. Use `#OWNER#` to reference this value in SQL queries and PL/SQL.  Note:  Changing `G_FLOW_OWNER` at runtime does not change the parsing schema. |
| `G_REQUEST` | Specifies the value of the request variable most recently passed to or set within the show or accept modules. |
| `G_BROWSER_LANGUAGE` | Refers to the web browser's current language preference. |
| `G_DEBUG` | Refers to whether debugging is switched on or off. Valid values for the DEBUG flag are `Yes` or `No`. Enabling debug shows details about application processing. |
| `G_HOME_LINK` | Refers to the home page of an application. If no page is given and if no alternative page is dictated by the authentication scheme's logic, the Oracle APEX engine redirects to this location. |
| `G_LOGIN_URL` | Used to display a link to a login page for users that are not currently logged in. |
| `G_IMAGE_PREFIX` | Refers to the virtual path the web server uses to point to the images directory distributed with APEX. |
| `G_FLOW_SCHEMA_OWNER` | Refers to the owner of the APEX schema. |
| `G_PRINTER_FRIENDLY` | Refers to whether the APEX engine is running in print view mode. This setting can be referenced in conditions to eliminate elements not desired in a printed document from a page. |
| `G_PROXY_SERVER` | Refers to the application attribute Proxy Server. |
| `G_SYSDATE` | Refers to the current date on the database server. `G_SYSDATE` uses the DATE datatype. |
| `G_PUBLIC_USER` | Refers to the Oracle schema used to connect to the database through the database access descriptor (DAD). |
| `G_GLOBAL_NOTIFICATION` | Specifies the application's global notification attribute. |
| `G_X01, ... G_X10` | Specifies the values of the `X01, ... X10` variables most recently passed to or set within the show or accept modules. You typically use these variables in On-Demand AJAX processes. |

---

## HELP Procedure

This procedure outputs page and item level help text as formatted HTML. You can also use it to customize how help information is displayed in your application.

Syntax

```sql
APEX_APPLICATION.HELP (
    p_request             IN VARCHAR2 DEFAULT NULL,
    p_flow_id             IN VARCHAR2 DEFAULT NULL,
    p_flow_step_id        IN VARCHAR2 DEFAULT NULL,
    p_show_item_help      IN VARCHAR2 DEFAULT 'YES',
    p_show_regions        IN VARCHAR2 DEFAULT 'YES',
    p_before_page_html    IN VARCHAR2 DEFAULT '<p>',
    p_after_page_html     IN VARCHAR2 DEFAULT NULL,
    p_before_region_html  IN VARCHAR2 DEFAULT NULL,
    p_after_region_html   IN VARCHAR2 DEFAULT '</td></tr></table></p>',
    p_before_prompt_html  IN VARCHAR2 DEFAULT '<p><b>',
    p_after_prompt_html   IN VARCHAR2 DEFAULT '</b></p>:&nbsp;',
    p_before_item_html    IN VARCHAR2 DEFAULT NULL,
    p_after_item_html     IN VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_request` | Not used. |
| `p_flow_id` | The application ID that contains the page or item level help you want to output. |
| `p_flow_step_id` | The page ID that contains the page or item level help you want to display. |
| `p_show_item_help` | Flag to determine if item-level help is output. If this parameter is supplied, the value must be either `YES` (default) or `NO`. |
| `p_show_regions` | Flag to determine if region headers are output (for regions containing page items). If this parameter is supplied, the value must be either `YES` (default) or `NO`. |
| `p_before_page_html` | Use this parameter to include HTML between the page-level help text and item-level help text. |
| `p_after_page_html` | Use this parameter to include HTML at the bottom of the output, after all other help. |
| `p_before_region_html` | Use this parameter to include HTML before every region section. This parameter is ignored if `p_show_regions` is set to `NO`. |
| `p_after_region_html` | Use this parameter to include HTML after every region section. This parameter is ignored if `p_show_regions` is set to `NO`. |
| `p_before_prompt_html` | Use this parameter to include HTML before every item label for item-level help. This parameter is ignored if `p_show_item_help` is set to `NO`. |
| `p_after_prompt_html` | Use this parameter to include HTML after every item label for item-level help. This parameter is ignored if `p_show_item_help` is set to `NO`. |
| `p_before_item_html` | Use this parameter to include HTML before every item help text for item-level help. This parameter is ignored if `p_show_item_help` is set to `NO`. |
| `p_after_item_html` | Use this parameter to include HTML after every item help text for item-level help. This parameter is ignored if `p_show_item_help` is set to `NO`. |

---

## STOP_APEX_ENGINE Procedure

This procedure signals the Oracle APEX engine to stop further processing and immediately exit to avoid adding additional HTML code to the HTTP buffer.

Note:

This procedure raises the exception `APEX_APPLICATION.E_STOP_APEX_ENGINE` internally. You must raise that exception again if you use a WHEN OTHERS exception handler.

Syntax

```sql
APEX_APPLICATION.STOP_APEX_ENGINE
```

Parameters

None.