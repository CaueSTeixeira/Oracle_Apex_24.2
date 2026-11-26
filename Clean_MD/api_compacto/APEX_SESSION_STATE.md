<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_SESSION_STATE (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_SESSION_STATE

The APEX_SESSION_STATE package encapsulates utilities needed to read and assign session state values.

---

## Global Constants

The the `t_value` record in the APEX_SESSION_STATE package uses the following data type constants.

```sql
subtype t_data_type is pls_integer range 1..11;

c_data_type_varchar2      constant t_data_type := apex_exec.c_data_type_varchar2;
c_data_type_clob          constant t_data_type := apex_exec.c_data_type_clob;
```

---

## Data Types

The APEX_SESSION_STATE package uses the following data types.

The `t_value` record type encapsulates a session state value. Only either `varchar2_value` or `clob_value` is populated at a time.

```sql
type t_value is record (
    data_type       t_data_type,
    varchar2_value  VARCHAR2(32767),
    clob_value      CLOB );
```

---

## GET_CLOB Function

This function returns the value of a CLOB item identified by `p_item`.

Syntax

```sql
APEX_SESSION_STATE.GET_CLOB (
    p_item IN VARCHAR2 )
RETURN CLOB;
```

Returns

This function returns the value of the specified item as CLOB.

---

## GET_NUMBER Function

This function returns the value of a page item identified by `p_item` as NUMBER. This function uses the item's format mask to perform the conversion.

Syntax

```sql
APEX_SESSION_STATE.GET_NUMBER (
    p_item IN VARCHAR2 )
RETURN NUMBER;
```

Returns

This function returns the value of the specified item as NUMBER.

---

## GET_TIMESTAMP Function

This function returns the value of a page item identified by `p_item` as TIMESTAMP. This function uses the item's format mask to perform the conversion.

Syntax

```sql
APEX_SESSION_STATE.GET_TIMESTAMP (
    p_item IN VARCHAR2 )
RETURN TIMESTAMP;
```

Returns

This function returns the value of the specified item as TIMESTAMP.

---

## GET_VALUE Function

This function returns the value of a page item identified by `p_item` as a generic T_VALUE.

Syntax

```sql
APEX_SESSION_STATE.GET_VALUE (
    p_item IN VARCHAR2 )
RETURN T_VALUE;
```

Returns

This function returns the value of the specified item as T_VALUE.

---

## GET_VARCHAR2 Function

This function returns the value of a VARCHAR2 item identified by `p_item`. This function is the equivalent of the V function. This function raises an exception for values of data type CLOB.

Syntax

```sql
APEX_SESSION_STATE.GET_VARCHAR2 (
    p_item IN VARCHAR2 )
RETURN VARCHAR2;
```

Returns

This function returns the value of the specified item as VARCHAR2.

---

## SET_VALUE Procedure Signature 1

This procedure sets an item's session state value based on VARCHAR2.

Syntax

```sql
APEX_SESSION_STATE.SET_VALUE (
    p_item   IN VARCHAR2,
    p_value  IN VARCHAR2,
    p_commit IN BOOLEAN DEFAULT TRUE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_item` | The item name. |
| `p_value` | The item value. |
| `p_commit` | If `TRUE` (default), commit after modifying the session state. If `FALSE`, or if the existing value in session state equals `p_value`, no commit is issued. This parameter is ignored when the application's Session State Changes attribute is set to "End Of Request." |

---

## SET_VALUE Procedure Signature 2

This procedure sets an item's session state value based on CLOB.

Syntax

```sql
APEX_SESSION_STATE.SET_VALUE (
    p_item   IN VARCHAR2,
    p_value  IN CLOB,
    p_commit IN BOOLEAN DEFAULT TRUE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_item` | The item name. |
| `p_value` | The item value. |
| `p_commit` | If `TRUE` (default), commit after modifying the session state. If `FALSE`, or if the existing value in session state equals `p_value`, no commit is issued. This parameter is ignored when the application's Session State Changes attribute is set to "End Of Request." |

---

## SET_VALUE Procedure Signature 3

This procedure sets an item's session state value based on a generic `t_value`.

Syntax

```sql
APEX_SESSION_STATE.SET_VALUE (
    p_item   IN VARCHAR2,
    p_value  IN t_value,
    p_commit IN BOOLEAN DEFAULT TRUE );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_item` | The item name. |
| `p_value` | The item value. |
| `p_commit` | If `TRUE` (default), commit after modifying the session state. If `FALSE`, or if the existing value in session state equals `p_value`, no commit is issued. This parameter is ignored when the application's Session State Changes attribute is set to "End Of Request." |