<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_STRING (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_STRING

The APEX_STRING package provides utilities for the following data types:


Unless otherwise noted, the APIs expect arrays to be continuous (that is, without holes that `coll.delete(n)` operations generate).

---

## FORMAT Function

This function returns a formatted string with substitutions applied.

Returns `p_message` after replacing each `<n>`th occurrence of `%s` with `p<n>` and each occurrence of `%<n>` with `p<n>`. If `p_max_length` is not null, `substr(p<n>,1,p_arg_max_length)` is used instead of `p<n>`.

Use `%%` in `p_message` to emit a single % character. Use %n to emit a newline.

Syntax

```sql
APEX_STRING.FORMAT (
     p_message    IN VARCHAR2,
     p0           IN VARCHAR2     DEFAULT NULL,
     p1           IN VARCHAR2     DEFAULT NULL,
     p2           IN VARCHAR2     DEFAULT NULL,
     p3           IN VARCHAR2     DEFAULT NULL,
     p4           IN VARCHAR2     DEFAULT NULL,
     p5           IN VARCHAR2     DEFAULT NULL,
     p6           IN VARCHAR2     DEFAULT NULL,
     p7           IN VARCHAR2     DEFAULT NULL,
     p8           IN VARCHAR2     DEFAULT NULL,
     p9           IN VARCHAR2     DEFAULT NULL,
     p10          IN VARCHAR2     DEFAULT NULL,
     p11          IN VARCHAR2     DEFAULT NULL,
     p12          IN VARCHAR2     DEFAULT NULL,
     p13          IN VARCHAR2     DEFAULT NULL,
     p14          IN VARCHAR2     DEFAULT NULL,
     p15          IN VARCHAR2     DEFAULT NULL,
     p16          IN VARCHAR2     DEFAULT NULL,
     p17          IN VARCHAR2     DEFAULT NULL,
     p18          IN VARCHAR2     DEFAULT NULL,
     p19          IN VARCHAR2     DEFAULT NULL,
     p_max_length IN PLS_INTEGER  DEFAULT 1000,
     p_prefix     IN VARCHAR2     DEFAULT NULL )
     return VARCHAR2
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_message` | Message string with substitution placeholders. |
| `p0-p19` | Substitution parameters. |
| `p_max_length` | If not null (default is 1000), cap each `p<n>` at `p_max_length` characters. The tilde (`~`) character is appended to indicate that the original value exceeded this length. |
| `p_prefix` | If set, remove leading white space and the given prefix from each line. This parameter can be used to simplify the formatting of indented multi-line text. |

---

## GET_INITIALS Function

Returns the initials of the words in a string.

Words are separated by spaces or other special characters such as:

* commas (,)
* dashes (-)
* quotes (')

If the input only has one word, returns the first characters of that word.

Syntax

```sql
APEX_STRING.GET_INITIALS (
   p_str IN VARCHAR2,
   p_cnt IN PLS_INTEGER DEFAULT 2 )
   RETURN VARCHAR2
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_string` | The input string. |
| `p_cnt` | The number (`N`) of letter initials to get from the first number (`N`) of words. Default `2`. Allowed values are 1 to 255. |

---

## GET_SEARCHABLE_PHRASES Function

This function returns distinct phrases of 1-3 consecutive lower case words in the input strings. Stopwords in the given language are ignored and split phrases.

Note:

This is a PL/SQL only implementation of a very small subset of what Oracle Text provides. Consider using Oracle Text instead, if the features and performance of this function are not sufficient.

Syntax

```sql
FUNCTION GET_SEARCHABLE_PHRASES (
    p_strings   IN   apex_t_varchar2,
    p_max_words IN   PLS_INTEGER     DEFAULT 3,
    p_language  IN   apex_t_varchar2 DEFAULT 'en' )
    RETURN apex_t_varchar2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_string` | The input string. |
| `p_max_words` | The maximum number of words in a phrase. The default is 3. |
| `p_language` | The language identifier for stopwords, defaults to `"en"`. Supported values are `"cn","de","en","es","fr","it","ja","ko","pt-br"`. |

---

## GREP Function Signature 1

Returns the values of the input table that match a regular expression.

Syntax

```sql
GREP (
   p_table         IN apex_t_varchar2,
   p_pattern       IN VARCHAR2,
   p_modifier      IN VARCHAR2    DEFAULT NULL,
   p_subexpression IN VARCHAR2    DEFAULT '0',
   p_limit         IN PLS_INTEGER DEFAULT NULL )
   RETURN apex_t_varchar2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_pattern` | The regular expression. |
| `p_modifier` | The regular expression modifier. |
| `p_subexpression` | The subexpression which should be returned. If null, return the complete table value. If 0 (the default), return the matched expression. If > 0, return the subexpression value. You can also pass a comma separated list of numbers, to get multiple subexpressions in the result. |
| `p_limit` | Limitation for the number of elements in the return table. If null (the default), there is no limit. |

---

## GREP Function Signature 2

Returns the values of the input `varchar2` that match a regular expression.

Syntax

```sql
APEX_STRING.GREP (
   p_str           IN VARCHAR2,
   p_pattern       IN VARCHAR2,
   p_modifier      IN VARCHAR2    DEFAULT NULL,
   p_subexpression IN VARCHAR2    DEFAULT '0',
   p_limit         IN PLS_INTEGER DEFAULT NULL )
   RETURN apex_t_varchar2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_str` | The input `varchar2`. |
| `p_pattern` | The regular expression. |
| `p_modifier` | The regular expression modifier. |
| `p_subexpression` | The subexpression which should be returned. If null, return the complete table value. If 0 (the default), return the matched expression. If > 0, return the subexpression value. You can also pass a comma separated list of numbers, to get multiple subexpressions in the result. |
| `p_limit` | Limitation for the number of elements in the return table. If null (the default), there is no limit. |

---

## GREP Function Signature 3

Returns the values of the input `clob` that match a regular expression.

Syntax

```sql
APEX_STRING.GREP (
   p_str           IN CLOB,
   p_pattern       IN VARCHAR2,
   p_modifier      IN VARCHAR2    DEFAULT NULL,
   p_subexpression IN VARCHAR2    DEFAULT '0',
   p_limit         IN PLS_INTEGER DEFAULT NULL )
   RETURN apex_t_varchar2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_str` | The input `clob`. |
| `p_pattern` | The regular expression. |
| `p_modifier` | The regular expression modifier. |
| `p_subexpression` | The subexpression which should be returned. If null, return the complete table value. If 0 (the default), return the matched expression. If > 0, return the subexpression value. You can also pass a comma separated list of numbers, to get multiple subexpressions in the result. |
| `p_limit` | Limitation for the number of elements in the return table. If null (the default), there is no limit. |

---

## INDEX_OF Function Signature 1

This function returns the first position in the list where `p_value` is stored. If not found, returns NULL.

Syntax

```sql
APEX_STRING.INDEX_OF (
    p_table IN apex_t_varchar2,
    p_value IN VARCHAR2 )
    RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | The table. |
| `p_value` | Value that is being searched for. |

Returns

Index of the searched value in the table.

---

## INDEX_OF Function Signature 2

This function returns the first position in the list where `p_value` is stored. If not found, returns NULL.

Syntax

```sql
APEX_STRING.INDEX_OF (
    p_table IN apex_application_global.vc_arr2,
    p_value IN VARCHAR2 )
    RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | The table. |
| `p_value` | Value that is being searched for. |

Returns

Index of the searched value in the table.

---

## JOIN_CLOB Function

Returns the values of the `apex_t_varchar2` input table `p_table` as a concatenated `clob`, separated by `p_sep`.

Syntax

```sql
APEX_STRING.JOIN_CLOB (
    p_table IN apex_t_varchar2,
    p_sep   IN VARCHAR2    DEFAULT apex_application.LF,
    p_dur   IN PLS_INTEGER DEFAULT sys.dbms_lob.call )
    RETURN CLOB
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_sep` | The separator, default is line feed. |
| `p_dur` | The duration of the `clob`, default `sys.dbms_lob.call` |

---

## JOIN_CLOBS Function

This function returns the values of the `apex_t_clob` input table `p_table` as a concatenated clob, separated by `p_sep`.

Syntax

```sql
APEX_STRING.JOIN_CLOBS (
  p_table IN apex_t_clob,
  p_sep   IN VARCHAR2     DEFAULT apex_application.LF,
  p_dur   IN PLS_INTEGER  DEFAULT sys.dbms_lob.call )
RETURN CLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_sep` | The separator, default is line feed. |
| `p_dur` | The duration of the clob, default `sys.dbms_lob.call` |

---

## JOIN Function Signature 1

Returns the values of the `apex_t_varchar2` input table `p_table` as a concatenated `varchar2`, separated by `p_sep`.

Syntax

```sql
APEX_STRING.JOIN (
   p_table IN apex_t_varchar2,
   p_sep IN VARCHAR2 DEFAULT apex_application.LF )
   RETURN VARCHAR2
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_sep` | The separator, default is line feed. |

---

## JOIN Function Signature 2

Returns the values of the `apex_t_number` input table `p_table` as a concatenated `varchar2`, separated by `p_sep`.

Syntax

```sql
APEX_STRING.JOIN (
   p_table IN apex_t_number,
   p_sep IN VARCHAR2 DEFAULT apex_application.LF )
   RETURN VARCHAR2
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_sep` | The separator, default is line feed. |

---

## NEXT_CHUNK Function

This function reads a fixed-length string from a clob. This is just a small wrapper around `DBMS_LOB.READ`, however it prevents common errors when incrementing the offset and picking the maximum chunk size.

Syntax

```sql
APEX_STRING.NEXT_CHUNK (
    p_str    IN            CLOB,
    p_chunk  OUT    NOCOPY VARCHAR2,
    p_offset IN OUT NOCOPY INTEGER,
    p_amount IN            INTEGER DEFAULT 8191 )
    RETURN BOOLEAN;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_str` | The input clob. |
| `p_chunk` | The chunk value (in/out). |
| `p_offset` | The position in `p_str`, where the next chunk should be read from (in/out). |
| `p_amount` | The amount of characters that should be read (default 8191). |

Returns

`True` if another chunk could be read. `False` if reading past the end of `p_str`.

---

## PLIST_DELETE Procedure

This procedure removes the property list key from the table.

Syntax

```sql
PLIST_DELETE (
    p_table IN OUT NOCOPY apex_t_varchar2,
    p_key   IN            VARCHAR2 );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_key` | The input key. |

Raised Errors

| Parameters | Description |
| --- | --- |
| `NO_DATA_FOUND` | Given key does not exist in table. |

---

## PLIST_EXISTS Function

Returns whether a key exists in the property list.

Syntax

```sql
APEX_STRING.PLIST_EXISTS (
    p_table IN apex_t_varchar2,
    p_key   IN VARCHAR2 )
    RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_key` | The input key. |

Raises

`NO_DATA_FOUND`: Given key does not exist in table.

---

## PLIST_GET Function

This function gets the property list value for a key.

Syntax

```sql
APEX_STRING.PLIST_GET (
    p_table IN apex_t_varchar2,
    p_key IN VARCHAR2 )
    RETURN VARCHAR2
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_key` | The input key. |

Raised Errors

| Parameters | Description |
| --- | --- |
| `NO_DATA_FOUND` | Given key does not exist in table. |

---

## PLIST_GET_KEY Function

Gets the first property list key that maps to a given value. Returns NULL if the value can not be found.

Syntax

```sql
APEX_STRING.PLIST_GET_KEY (
    p_table IN apex_t_varchar2,
    p_value IN VARCHAR2 )
    RETURN varchar2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_value` | The input value. |

---

## PLIST_PUSH Procedure

This procedure appends key/value to the property list, without looking for duplicates.

Syntax

```sql
APEX_STRING.PLIST_PUSH (
    p_table IN OUT NOCOPY apex_t_varchar2,
    p_key   IN VARCHAR2,
    p_value IN VARCHAR2 );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_key` | The input key. |
| `p_value` | The input value. |

---

## PLIST_PUT Function

This function inserts or updates property list value for a key.

Syntax

```sql
PLIST_PUT (
    p_table IN OUT NOCOPY apex_t_varchar2,
    p_key   IN            VARCHAR2,
    p_value IN            VARCHAR2 );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_key` | The input key. |
| `p_value` | The input value. |

---

## PLIST_TO_JSON_CLOB Function

This function converts a `apex_t_varchar2` record to a `sys.json_object_t` object type and stringifies it.

Elements with odd numbers are the attribute names.

Elements with even numbers are the attribute values.

Syntax

```sql
APEX_STRING.PLIST_TO_JSON_CLOB (
    p_plist IN apex_t_varchar2 )
RETURN CLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_plist` | The table. |

Returns

CLOB containing a JSON object with keys and values of the given `p_plist`.

---

## PUSH Procedure Signature 1

This procedure appends value to `apex_t_varchar2` table.

Syntax

```sql
APEX_STRING.PUSH (
   p_table IN OUT NOCOPY apex_t_varchar2,
   p_value IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | Defines the table. |
| `p_value` | Specifies the value to be added. |

---

## PUSH Procedure Signature 2

This procedure appends a value to `apex_t_clob` table.

Syntax

```sql
APEX_STRING.PUSH (
   p_table IN OUT NOCOPY apex_t_clob,
   p_value IN            apex_t_clob );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | Defines the table. |
| `p_value` | Specifies the value to be added. |

---

## PUSH Procedure Signature 3

This procedure appends a value to `apex_t_number` table.

Syntax

```sql
APEX_STRING.PUSH (
   p_table IN OUT NOCOPY apex_t_number,
   p_value IN            NUMBER );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | Defines the table. |
| `p_value` | Specifies the value to be added. |

---

## PUSH Procedure Signature 4

This procedure appends collection values to `apex_t_varchar2` table.

Syntax

```sql
APEX_STRING. PUSH (
   p_table  IN OUT NOCOPY apex_t_varchar2,
   p_values IN            apex_t_varchar2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | Defines the table. |
| `p_values` | Specifies the values that should be added to `p_table`. |

---

## PUSH Procedure Signature 5

This procedure appends collection values to the `apex_t_clob` table.

Syntax

```sql
APEX_STRING.PUSH (
  p_table  IN OUT NOCOPY apex_t_clob,
  p_values IN            apex_t_clob )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | The table. |
| `p_values` | Values to be added to `p_table`. |

---

## PUSH Procedure Signature 6

This procedure appends values of a PL/SQL table to the `apex_t_varchar2` table.

Syntax

```sql
APEX_STRING.PUSH (
  p_table  IN OUT NOCOPY apex_t_varchar2,
  p_values IN            apex_application_global.vc_arr2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | The table. |
| `p_values` | Values to add to `p_table`. |

---

## PUSH Procedure Signature 7

This procedure appends number collection values to the `apex_t_varchar2` table.

Syntax

```sql
APEX_STRING.PUSH (
    p_table         IN OUT NOCOPY apex_t_varchar2,
    p_values        IN            apex_t_number,
    p_format_mask   IN            VARCHAR2 DEFAULT NULL );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | The table. |
| `p_values` | Values that should be added to `p_table`. |
| `p_format_mask` | Format mask to use when converting numbers to strings. |

---

## SHUFFLE Function

Returns the input table values, re-ordered.

Syntax

```sql
APEX_STRING.SHUFFLE (
    p_table IN apex_t_varchar2 )
    RETURN apex_t_varchar2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table. |

---

## SHUFFLE Procedure

This procedure randomly re-orders the values of the input table.

Syntax

```sql
APEX_STRING.SHUFFLE (
    p_table IN OUT NOCOPY apex_t_varchar2 );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table, which will be modified by the procedure. |

---

## SPLIT Function Signature 1

Use this function to split input string at separator.

Syntax

```sql
APEX_STRING.SPLIT (
    p_str   IN VARCHAR2,
    p_sep   IN VARCHAR2     DEFAULT apex_application.LF,
    p_limit IN PLS_INTEGER  DEFAULT NULL )
    RETURN apex_t_varchar2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_str` | The input string. |
| `p_sep` | The separator. Splits at line feed by default.  If null, split after each character. If a single character, split at this character. If more than 1 character, split at regular expression (max 512 characters). |
| `p_limit` | Maximum number of splits, ignored if null. If smaller than the total possible number of splits, the last table element contains the rest. |

---

## SPLIT Function Signature 2

Use this function to split input clob at separator.

Syntax

```sql
APEX_STRING.SPLIT (
    p_str IN CLOB,
    p_sep IN VARCHAR2 DEFAULT apex_application.LF )
    RETURN apex_t_varchar2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_str` | The input clob. |
| `p_sep` | The separator. Splits at line feed by default.  If null, split after each character. If a single character, split at this character. If more than 1 character, split at regular expression (max 512 characters). |

---

## SPLIT_CLOBS Function

This function splits input clobs at the separator and returns a table of clobs.

Syntax

```sql
APEX_STRING.SPLIT_CLOBS (
  p_str   IN CLOB,
  p_sep   IN VARCHAR2    DEFAULT apex_application.LF,
  p_limit IN PLS_INTEGER DEFAULT NULL )
RETURN apex_t_clob;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_str` | The input clob. |
| `p_sep` | The separator. Splits at line feed by default.  If null, split after each character. If a single character, split at this character. If more than 1 character, split at regular expression (max 512 characters). |
| `p_limit` | Maximum number of splits. Ignored if null.  If smaller than the total possible number of splits, the last table element contains the rest. |

---

## SPLIT_NUMBERS Function

Use this function to split input at separator, values must all be numbers.

Syntax

```sql
SPLIT_NUMBERS (
     p_str IN VARCHAR2,
     p_sep IN VARCHAR2 DEFAULT apex_application.LF )
     RETURN apex_t_number;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_str` | The input varchar2. |
| `p_sep` | The separator. Splits at line feed by default.  If null, split after each character. If a single character, split at this character. If more than 1 character, split at regular expression (max 512 characters). |

---

## STRING_TO_TABLE Function

This function returns the split input at separator, returning a `vc_arr2`.

Syntax

```sql
APEX_STRING.STRING_TO_TABLE (
    p_str   IN VARCHAR2,
    p_sep   IN VARCHAR2 DEFAULT ':' )
    RETURN apex_application_global.vc_arr2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_str` | The input varchar2. |
| `p_sep` | The separator, no regexp or split at char. Defaults to `':'`. |

---

## TABLE_TO_CLOB Function

This function returns the values of the `apex_application_global.vc_arr2` input table `p_table` as a concatenated clob, separated by `p_sep`.

Syntax

```sql
APEX_STRING.TABLE_TO_CLOB (
    p_table IN apex_application_global.vc_arr2,
    p_sep   IN VARCHAR2             DEFAULT apex_application.LF,
    p_dur   IN PLS_INTEGER          DEFAULT sys.dbms_lob.call )
    RETURN CLOB;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_table` | The input table. |
| `p_sep` | The separator. Default is line feed. |
| `p_dur` | The duration of the clob. Default `sys.dbms_lob.call`. |

---

## TABLE_TO_STRING Function

This function returns the values of the `apex_application_global.vc_arr2` input table `p_table` as a concatenated `varchar2`, separated by `p_sep`.

Syntax

```sql
APEX_STRING.TABLE_TO_STRING (
    p_table IN apex_application_global.vc_arr2,
    p_sep   IN VARCHAR2             DEFAULT ':' )
    RETURN VARCHAR2;
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_table` | The input table, assumes no holes and index starts at 1. |
| `p_sep` | The separator, default is `':'`. |