<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_COLLECTION (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_COLLECTION

Collections enable you to temporarily capture one or more nonscalar values. You can use collections to store rows and columns currently in session state so they can be accessed, manipulated, or processed during a user's specific session. You can think of a collection as a bucket in which you temporarily store and name rows of information.

---

## About the APEX_COLLECTION API

Every collection contains a named list of data elements (or members) which can have up to 50 character attributes (`VARCHAR2(4000)`), five number attributes, five date attributes, one XML Type attribute, one large binary attribute (`BLOB`), and one large character attribute (`CLOB`). You insert, update, and delete collection information using the PL/SQL API `APEX_COLLECTION`.

The following are examples of when you might use collections:

* When you are creating a data-entry wizard in which multiple rows of information first need to be collected within a logical transaction. You can use collections to temporarily store the contents of the multiple rows of information, before performing the final step in the wizard when both the physical and logical transactions are completed.
* When your application includes an update page on which a user updates multiple detail rows on one page. The user can make many updates, apply these updates to a collection and then call a final process to apply the changes to the database.
* When you are building a wizard where you are collecting an arbitrary number of attributes. At the end of the wizard, the user then performs a task that takes the information temporarily stored in the collection and applies it to the database.

Beginning in Oracle
Database 12c, database columns of data type `VARCHAR2` can be defined up to 32,767 bytes. This requires that the database initialization parameter `MAX_STRING_SIZE` has a value of `EXTENDED`. If Oracle APEX was installed in Oracle
Database 12c and with `MAX_STRING_SIZE=EXTENDED`, then the tables for the APEX collections will be defined to support up 32,767 bytes for the character attributes of a collection. For the methods in the APEX_COLLECTION API, all references to character attributes (`c001` through `c050`) can support up to 32,767 bytes.

* Accessing a Collection
* Determining Collection Status
* Clearing Collection Session State

---

## ADD_MEMBER Procedure

Adds a new member to an existing collection. An error occurs if the specified collection does not exist for the current user in the same session for the current application ID.

Gaps are not used when adding a new member, so an existing collection with members of sequence IDs (1,2,5,8) adds the new member with a sequence ID of 9.

Syntax

```sql
APEX_COLLECTION.ADD_MEMBER (
    p_collection_name   IN VARCHAR2,
    p_c001              IN VARCHAR2 DEFAULT NULL,
    ...
    p_c050              IN VARCHAR2 DEFAULT NULL,
    p_n001              IN NUMBER   DEFAULT NULL,
    p_n002              IN NUMBER   DEFAULT NULL,
    p_n003              IN NUMBER   DEFAULT NULL,
    p_n004              IN NUMBER   DEFAULT NULL,
    p_n005              IN NUMBER   DEFAULT NULL,
    p_d001              IN DATE     DEFAULT NULL,
    p_d002              IN DATE     DEFAULT NULL,
    p_d003              IN DATE     DEFAULT NULL,
    p_d004              IN DATE     DEFAULT NULL,
    p_d005              IN DATE     DEFAULT NULL,
    p_clob001           IN CLOB     DEFAULT empty_clob(),
    p_blob001           IN BLOB     DEFAULT empty_blob(),
    p_xmltype001        IN XMLTYPE  DEFAULT NULL,
    p_generate_md5      IN VARCHAR2 DEFAULT 'NO' )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of an existing collection. Maximum length is 255 bytes. Collection names are not case-sensitive and are converted to upper case. |
| `p_c001 through p_c050` | Attribute value of the member to be added. Maximum length is 4,000 bytes. Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. |
| `p_n001 through p_n005` | Attribute value of the numeric attributes to be added. |
| `p_d001` through `p_d005` | Attribute value of the date attribute. |
| `p_clob001` | Use for collection member attributes that exceed 4,000 characters. |
| `p_blob001` | Use for binary collection member attributes. |
| `p_xmltype001` | Use to store well-formed XML. |
| `p_generate_md5` | Valid values include `YES` and `NO`. `YES` to specify if the message digest of the data of the collection member should be computed. Use this parameter to compare the MD5 of the collection member with another member or to see if that member has changed. |

---

## ADD_MEMBER Function

Adds a new member to an existing collection. Calling this function returns the sequence ID of the newly added member. An error occurs if the specified collection does not exist for the current user in the same session for the current application ID.

Gaps are not used when adding a new member, so an existing collection with members of sequence IDs (1,2,5,8) adds the new member with a sequence ID of 9.

Syntax

```sql
APEX_COLLECTION.ADD_MEMBER (
    p_collection_name   IN VARCHAR2,
    p_c001              IN VARCHAR2 DEFAULT NULL,
    ...
    p_c050              IN VARCHAR2 DEFAULT NULL,
    p_n001              IN NUMBER   DEFAULT NULL,
    p_n002              IN NUMBER   DEFAULT NULL,
    p_n003              IN NUMBER   DEFAULT NULL,
    p_n004              IN NUMBER   DEFAULT NULL,
    p_n005              IN NUMBER   DEFAULT NULL,
    p_d001              IN DATE     DEFAULT NULL,
    p_d002              IN DATE     DEFAULT NULL,
    p_d003              IN DATE     DEFAULT NULL,
    p_d004              IN DATE     DEFAULT NULL,
    p_d005              IN DATE     DEFAULT NULL,
    p_clob001           IN CLOB     DEFAULT empty_clob(),
    p_blob001           IN BLOB     DEFAULT empty_blob(),
    p_xmltype001        IN XMLTYPE  DEFAULT NULL,
    p_generate_md5      IN VARCHAR2 DEFAULT 'NO' )
RETURN NUMBER;
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of an existing collection. Maximum length is 255 bytes. Collection names are not case sensitive and are converted to upper case. |
| `p_c001 through p_c050` | Attribute value of the member to be added. Maximum length is 4,000 bytes. Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. |
| `p_n001 through p_n005` | Attribute value of the numeric attributes to be added. |
| `p_d001` through `p_d005` | Attribute value of the date attribute to be added. |
| `p_clob001` | Use for collection member attributes that exceed 4,000 characters. |
| `p_blob001` | Use for binary collection member attributes. |
| `p_xmltype001` | Use to store well-formed XML. |
| `p_generate_md5` | Valid values include `YES` and `NO`. `YES` to specify if the message digest of the data of the collection member should be computed. Use this parameter to compare the MD5 of the collection member with another member or to see if that member has changed. |

---

## ADD_MEMBERS Procedure

Adds an array of members to a collection. An error occurs if the specified collection does not exist for the current user in the same session for the current application ID.

Gaps are not used when adding a new member, so an existing collection with members of sequence IDs (1,2,5,8) adds the new member with a sequence ID of 9.

The count of elements in the `p_c001` PL/SQL table is used as the total number of items across all PL/SQL tables. For example, if `p_c001.count` is 2 and `p_c002.count` is 10, only 2 members are added. If `p_c001` is NULL, an application error occurs.

Syntax

```sql
APEX_COLLECTION.ADD_MEMBERS (
  p_collection_name IN VARCHAR2,
  p_c001            IN apex_application_global.vc_arr2,
  p_c002            IN apex_application_global.vc_arr2  DEFAULT empty_vc_arr,
  p_c003            IN apex_application_global.vc_arr2  DEFAULT empty_vc_arr,
  ...
  p_c050            IN apex_application_global.vc_arr2  DEFAULT empty_vc_arr,
  p_n001            IN apex_application_global.n_arr    DEFAULT empty_n_arr,
  p_n002            IN apex_application_global.n_arr    DEFAULT empty_n_arr,
  p_n003            IN apex_application_global.n_arr    DEFAULT empty_n_arr,
  p_n004            IN apex_application_global.n_arr    DEFAULT empty_n_arr,
  p_n005            IN apex_application_global.n_arr    DEFAULT empty_n_arr,
  p_d001            IN apex_application_global.d_arr    DEFAULT empty_d_arr,
  p_d002            IN apex_application_global.d_arr    DEFAULT empty_d_arr,
  p_d003            IN apex_application_global.d_arr    DEFAULT empty_d_arr,
  p_d004            IN apex_application_global.d_arr    DEFAULT empty_d_arr,
  p_d005            IN apex_application_global.d_arr    DEFAULT empty_d_arr,
  p_generate_md5    IN VARCHAR2                         DEFAULT 'NO' )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. The number of members added is based on the number of elements in the first array.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of an existing collection. Maximum length is 255 bytes. Collection names are not case sensitive and are converted to upper case. |
| `p_c001` through `p_c050` | Array of character attribute values to be added. |
| `p_n001` through `p_n005` | Array of numeric attribute values to be added. |
| `p_d001` through `p_d005` | Array of date attribute values to be added. |
| `p_generate_md5` | Valid values include `YES` and `NO`. `YES` to specify if the message digest of the data of the collection member should be computed. Use this parameter to compare the MD5 of the collection member with another member or to see if that member has changed. |

---

## COLLECTION_EXISTS Function

Determines if a collection exists. Returns `TRUE` if the specified collection exists for the current user in the current session for the current application ID, otherwise `FALSE`.

Syntax

```sql
APEX_COLLECTION.COLLECTION_EXISTS (
    p_collection_name   IN VARCHAR2 )
RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. Maximum length is 255 bytes. The collection name is not case-sensitive and is converted to upper case. |

---

## COLLECTION_HAS_CHANGED Function

Determines if a collection has changed since it was created or since the collection changed flag was reset.

Syntax

```sql
APEX_COLLECTION.COLLECTION_HAS_CHANGED (
    p_collection_name   IN VARCHAR2 )
RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |

---

## COLLECTION_MEMBER_COUNT Function

Retrieves the total number of members for the named collection. If gaps exist, the total member count returned is not equal to the highest sequence ID in the collection.

If the named collection does not exist for the current user in the current session, no error occurs.

Syntax

```sql
APEX_COLLECTION.COLLECTION_MEMBER_COUNT (
    p_collection_name   IN VARCHAR2 )
RETURN NUMBER;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. |

---

## CREATE_COLLECTION Procedure

Creates an empty collection that does not already exist. If a collection exists with the same name for the current user in the same session for the current application ID, an application error occurs.

Syntax

```sql
APEX_COLLECTION.CREATE_COLLECTION (
    p_collection_name       IN VARCHAR2,
    p_truncate_if_exists    IN VARCHAR2 DEFAULT 'NO' )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. The maximum length is 255 characters. An error is returned if this collection exists with the specified name of the current user and in the same session. |
| `p_truncate_if_exists` | If `YES`, then members of the collection are first truncated if the collection exists and no error occurs. If `NO` (or not `YES`), and the collection exists, an error occurs. |

---

## CREATE_COLLECTION_FROM_QUERY Procedure

Creates a collection from a supplied query. The query is parsed as the application owner.

This method can be used with a query with up to 50 columns in the `SELECT` clause. These columns in the `SELECT` clause populate the 50 character attributes of the collection (`C001` through `C050`).

If a collection exists with the same name for the current user in the same session for the current Application ID, an application error occurs.

Syntax

```sql
APEX_COLLECTION.CREATE_COLLECTION_FROM_QUERY (
    p_collection_name       IN VARCHAR2,
    p_query                 IN VARCHAR2,
    p_generate_md5          IN VARCHAR2 DEFAULT 'NO',
    p_truncate_if_exists    IN VARCHAR2 DEFAULT 'NO' )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. The maximum length is 255 characters. An error is returned if this collection exists with the specified name of the current user and in the same session. |
| `p_query` | Query to execute to populate the members of the collection. |
| `p_generate_md5` | Valid values include `YES` and `NO`. `YES` to specify if the message digest of the data of the collection member should be computed. Use this parameter to compare the MD5 of the collection member with another member or to see if that member has changed. |
| `p_truncate_if_exists` | If `YES`, then members of the collection are first truncated if the collection exists and no error occurs. If `NO` (or not `YES`), and the collection exists, an error occurs. |

---

## CREATE_COLLECTION_FROM_QUERY2 Procedure

Creates a collection from a supplied query.

This method is identical to `CREATE_COLLECTION_FROM_QUERY`, however, the first 5 columns of the `SELECT` clause must be numeric and the next 5 must be date. After the numeric and date columns, there can be up to 50 character columns in the `SELECT` clause. The query is parsed as the application owner.

If a collection exists with the same name for the current user in the same session for the current application ID, an application error is raised.

Syntax

```sql
APEX_COLLECTION.CREATE_COLLECTION_FROM_QUERY2 (
    p_collection_name       IN VARCHAR2,
    p_query                 IN VARCHAR2,
    p_generate_md5          IN VARCHAR2 DEFAULT 'NO',
    p_truncate_if_exists    IN VARCHAR2 DEFAULT 'NO' )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. The maximum length is 255 characters. An error is returned if this collection exists with the specified name of the current user and in the same session. |
| `p_query` | Query to execute to populate the members of the collection. |
| `p_generate_md5` | Valid values include `YES` and `NO`. `YES` to specify if the message digest of the data of the collection member should be computed. Use this parameter to compare the MD5 of the collection member with another member or to see if that member has changed. |
| `p_truncate_if_exists` | If `YES`, then members of the collection will first be truncated if the collection exists and no error will be raised. If `NO` (or not `YES`), and the collection exists, an error will be raised. |

---

## CREATE_COLLECTION_FROM_QUERY_B Procedure

Creates a collection from a supplied query using bulk operations.

This method offers significantly faster performance than the `CREATE_COLLECTION_FROM_QUERY` method. The query is parsed as the application owner. If a collection exists with the same name for the current user in the same session for the current application ID, an application error occurs.

This procedure uses bulk dynamic SQL to perform the fetch and insert operations into the named collection. Two limitations are imposed by this procedure:

1. The MD5 checksum for the member data is not computed.
2. No column value in query `p_query` can exceed 2,000 bytes. If a row is encountered that has a column value of more than 2,000 bytes, an error is raised during execution. In Oracle
   Database 11g Release 2 (11.2.0.1) or later, this column limit is 4,000 bytes.

Syntax

```sql
APEX_COLLECTION.CREATE_COLLECTION_FROM_QUERY_B (
    p_collection_name       IN VARCHAR2,
    p_query                 IN VARCHAR2,
    p_names                 IN apex_application_global.vc_arr2,
    p_values                IN apex_application_global.vc_arr2,
    p_max_row_count         IN NUMBER   DEFAULT NULL,
    p_truncate_if_exists    IN VARCHAR2 DEFAULT 'NO' )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. The maximum length is 255 characters. An error is returned if this collection exists with the specified name of the current user and in the same session. |
| `p_query` | Query to execute to populate the members of the collection. |
| `p_names` | Array of bind variable names used in the query statement. |
| `p_values` | Array of bind variable values used in the bind variables in the query statement. |
| `p_max_row_count` | Maximum number of rows returned from the query in `p_query` to add to the collection. |
| `p_truncate_if_exists` | If `YES`, then members of the collection are truncated first if the collection exists and no error occurs. If `NO` (or not `YES`), and the collection exists, an error occurs. |

---

## CREATE_COLLECTION_FROM_QUERY_B Procedure (No bind version)

Creates a collection from a supplied query using bulk operations.

This method offers significantly faster performance than the `CREATE_COLLECTION_FROM_QUERY` method. The query is parsed as the application owner. If a collection exists with the same name for the current user in the same session for the current application ID, an application error occurs.

This procedure uses bulk dynamic SQL to perform the fetch and insert operations into the named collection. Two limitations are imposed by this procedure:

1. The MD5 checksum for the member data is not computed.
2. No column value in query `p_query` can exceed 2,000 bytes. If a row is encountered that has a column value of more than 2,000 bytes, an error occurs during execution. In Oracle
   Database 11g Release 2 (11.2.0.1) or later, this column limit is 4,000 bytes.

Syntax

```sql
 APEX_COLLECTION.CREATE_COLLECTION_FROM_QUERY_B (
    p_collection_name   IN VARCHAR2,
    p_query             IN VARCHAR2,
    p_max_row_count     IN NUMBER   DEFAULT NULL )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. The maximum length is 255 characters. An error is returned if this collection exists with the specified name of the current user and in the same session. |
| `p_query` | Query to execute to populate the members of the collection. |
| `p_max_row_count` | Maximum number of rows returned from the query in `p_query` to be added to the collection. |

---

## CREATE_COLLECTION_FROM_QUERYB2 Procedure

Creates a collection from a supplied query using bulk operations.

This method offers significantly faster performance than the `CREATE_COLLECTION_FROM_QUERY_2` method. The query is parsed as the application owner. If a collection exists with the same name for the current user in the same session for the current application ID, an application error occurs.

This procedure is identical to `CREATE_COLLECTION_FROM_QUERY_B` except the first five columns of the `SELECT` clause must be numeric and the next five columns must be a date. After the date columns, there can be up to 50 character columns in the `SELECT` clause.

This procedure uses bulk dynamic SQL to perform the fetch and insert operations into the named collection. Two limitations are imposed by this procedure:

1. The MD5 checksum for the member data is not computed.
2. No column value in query `p_query` can exceed 2,000 bytes. If a row is encountered that has a column value of more than 2,000 bytes, an error is raised during execution. In Oracle
   Database 11g Release 2 (11.2.0.1) or later, this column limit is 4,000 bytes.

Syntax

```sql
APEX_COLLECTION.CREATE_COLLECTION_FROM_QUERYB2 (
    p_collection_name       IN VARCHAR2,
    p_query                 IN VARCHAR2,
    p_names                 IN apex_application_global.vc_arr2,
    p_values                IN apex_application_global.vc_arr2,
    p_max_row_count         IN NUMBER   DEFAULT NULL,
    p_truncate_if_exists    IN VARCHAR2 DEFAULT 'NO' )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. The maximum length is 255 characters. An error is returned if this collection exists with the specified name of the current user and in the same session. |
| `p_query` | Query to execute to populate the members of the collection. |
| `p_names` | Array of bind variable names used in the query statement. |
| `p_values` | Array of bind variable values used in the bind variables in the query statement. |
| `p_max_row_count` | Maximum number of rows returned from the query in `p_query` to be added to the collection. |
| `p_truncate_if_exists` | If `YES`, then members of the collection are first truncated if the collection exists. If `NO` (or not `YES`), and the collection exists, an error occurs. |

---

## CREATE_COLLECTION_FROM_QUERYB2 Procedure (No bind version)

Creates a collection from a supplied query using bulk operations.

This method offers significantly faster performance than the `CREATE_COLLECTION_FROM_QUERY_2` method. The query is parsed as the application owner. If a collection exists with the same name for the current user in the same session for the current application ID, an application error occurs.

This procedure is identical to `CREATE_COLLECTION_FROM_QUERY_B` except the first five columns of the `SELECT` clause must be numeric and the next five columns must be a date. After the date columns, there can be up to 50 character columns in the `SELECT` clause.

This procedure uses bulk dynamic SQL to perform the fetch and insert operations into the named collection. Two limitations are imposed by this procedure:

1. The MD5 checksum for the member data is not computed.
2. No column value in query `p_query` can exceed 2,000 bytes. If a row is encountered that has a column value of more than 2,000 bytes, an error is raised during execution. In Oracle
   Database 11g Release 2 (11.2.0.1) or later, this column limit is 4,000 bytes.

Syntax

```sql
APEX_COLLECTION.CREATE_COLLECTION_FROM_QUERYB2 (
    p_collection_name   IN VARCHAR2,
    p_query             IN VARCHAR2,
    p_max_row_count     IN NUMBER   DEFAULT )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. The maximum length is 255 characters. An error is returned if this collection exists with the specified name of the current user and in the same session. |
| `p_query` | Query to execute to populate the members of the collection. |
| `p_max_row_count` | Maximum number of rows returned from the query in `p_query` to be added to the collection. |

---

## CREATE_OR_TRUNCATE_COLLECTION Procedure

Creates a collection. If a collection exists with the same name for the current user in the same session for the current application ID, all members of the collection are removed (the named collection is truncated).

Syntax

```sql
APEX_COLLECTION.CREATE_OR_TRUNCATE_COLLECTION (
    p_collection_name   IN VARCHAR2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. The maximum length is 255 characters. All members of the named collection are removed if the named collection exists for the current user in the current session. |

---

## DELETE_ALL_COLLECTIONS Procedure

Use this procedure to delete all collections that belong to the current user in the current Oracle APEX session for the current Application ID.

Syntax

```sql
APEX_COLLECTION.DELETE_ALL_COLLECTIONS;
```

Parameters

None.

---

## DELETE_ALL_COLLECTIONS_SESSION Procedure

Use this procedure to delete all collections that belong to the current user in the current Oracle APEX session regardless of the Application ID.

Syntax

```sql
APEX_COLLECTION.DELETE_ALL_COLLECTIONS_SESSION;
```

Parameters

None.

---

## DELETE_COLLECTION Procedure

Deletes a named collection. All members that belong to the collection are removed and the named collection is dropped.

If the named collection does not exist for the same user in the current session for the current application ID, an application error occurs.

Syntax

```sql
APEX_COLLECTION.DELETE_COLLECTION (
    p_collection_name   IN VARCHAR2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection to remove all members from and drop. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |

---

## DELETE_MEMBER Procedure

Deletes a specified member from a given named collection.

If the named collection does not exist for the same user in the current session for the current application ID, an application error occurs.

Syntax

```sql
APEX_COLLECTION.DELETE_MEMBER (
    p_collection_name   IN VARCHAR2,
    p_seq               IN VARCHAR2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection to delete the specified member from. The maximum length is 255 characters. Collection names are not case-sensitive and are converted to upper case. An error is returned if this collection does not exist for the current user in the same session. |
| `p_seq` | This is the sequence ID of the collection member to be deleted. |

---

## DELETE_MEMBERS Procedure

Deletes all members from a given named collection where the attribute specified by the attribute number equals the supplied value.

If the named collection does not exist for the same user in the current session for the current application ID, an application error occurs.

If the attribute number specified is invalid or outside the range of 1 to 50, an error occurs.

If the supplied attribute value is NULL, then all members of the named collection are deleted where the attribute, specified by `p_attr_number`, is NULL.

Syntax

```sql
APEX_COLLECTION.DELETE_MEMBERS (
    p_collection_name   IN VARCHAR2,
    p_attr_number       IN NUMBER,
    p_attr_value        IN VARCHAR2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection to delete the specified members from. The maximum length is 255 characters. Collection names are not case-sensitive and are converted to upper case. An error is returned if this collection does not exist for the current user in the same session. |
| `p_attr_number` | Attribute number of the member attribute used to match for the specified attribute value for deletion. Valid values are 1 through 50 and NULL. |
| `p_attr_value` | Attribute value of the member attribute used to match for deletion. Maximum length can be 4,000 bytes. The attribute value is truncated to 4,000 bytes if greater than this amount. |

---

## GET_MEMBER_MD5 Function

Computes and returns the message digest of the attributes for the member specified by the sequence ID. This computation of message digest is equal to the computation performed natively by collections. The result of this function can be compared to the `MD5_ORIGINAL` column of the view `APEX_COLLECTIONS`.

If a collection does not exist with the specified name for the current user in the same session and for the current application ID, an application error occurs.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

Syntax

```sql
APEX_COLLECTION.GET_MEMBER_MD5 (
    p_collection_name   IN VARCHAR2,
    p_seq               IN NUMBER )
RETURN VARCHAR2;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection to add this array of members to. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |
| `p_seq` | Sequence ID of the collection member. |

---

## MERGE_MEMBERS Procedure

Merges members of the given named collection with the values passed in the arrays.

If the named collection does not exist, one is created.

If a `p_init_query` is provided, the collection is created from the supplied SQL query.

If the named collection exists, the following occurs:

1. Rows in the collection and not in the arrays are deleted.
2. Rows in the collections and in the arrays are updated.
3. Rows in the arrays and not in the collection are inserted.

The count of elements in the `p_c001` PL/SQL table is used as the total number of items across all PL/SQL tables. For example, if `p_c001.count` is `2` and `p_c002.count` is `10`, only two members are merged.

If `p_c001` is NULL, an application error occurs.

Syntax

```sql
APEX_COLLECTION.MERGE_MEMBERS (
    p_collection_name   IN VARCHAR2,
    p_seq               IN apex_application_global.vc_arr2 DEFAULT empty_vc_arr,
    p_c001              IN apex_application_global.vc_arr2 DEFAULT empty_vc_arr,
    p_c002              IN apex_application_global.vc_arr2 DEFAULT empty_vc_arr,
    p_c003              IN apex_application_global.vc_arr2 DEFAULT empty_vc_arr,
    ...
    p_c050              IN apex_application_global.vc_arr2 DEFAULT empty_vc_arr,
    p_null_index        IN NUMBER   DEFAULT 1,
    p_null_value        IN VARCHAR2 DEFAULT NULL,
    p_init_query        IN VARCHAR2 DEFAULT NULL )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. Also, the number of members added is based on the number of elements in the first array.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. Maximum length is 255 bytes. Collection names are not case-sensitive and are converted to upper case. |
| `p_c001 through p_c050` | Array of attribute values to be merged. Maximum length is 4,000 bytes. Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. The count of the `p_c001` array is used across all arrays. If no values are provided, then no actions are performed. |
| `p_c0xx` | Attribute of `NN` attributes values to be merged. Maximum length can be 4,000 bytes. The attribute value is truncated to 4,000 bytes if greater than this amount. |
| `p_seq` | Identifies the sequence number of the collection member to be merged. |
| `p_null_index` | If the element identified by this value is NULL, then treat this row as a NULL row. For example, if `p_null_index` is `3`, then `p_c003` is treated as a NULL row. The merge function then ignores this row. This results in removing NULL rows from the collection. The NULL index works with the NULL value. If the value of the `p_cXXX` argument is equal to the `p_null_value`, then the row is treated as NULL. |
| `p_null_value` | Used with the `p_null_index` argument. Identifies the NULL value. If used, this value must not be NULL. A typical value for this argument is `0`. |
| `p_init_query` | If the collection does not exist, the collection is created using this query. |

---

## MOVE_MEMBER_DOWN Procedure

Adjusts the sequence ID of a specified member in the given named collection down by one (subtract one), swapping sequence ID with the one it is replacing. For example, 3 becomes 2 and 2 becomes 3.

If a collection does not exist with the specified name for the current user in the same session and for the current application ID, an application error is raised.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

If the member specified by sequence ID `p_seq` is the lowest sequence in the collection, an application error is NOT returned.

Syntax

```sql
APEX_COLLECTION.MOVE_MEMBER_DOWN (
    p_collection_name   IN VARCHAR2,
    p_seq               IN NUMBER )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. Maximum length is 255 bytes. Collection names are not case-sensitive and are converted to upper case. An error is returned if this collection does not exist with the specified name of the current user in the same session. |
| `p_seq` | Identifies the sequence number of the collection member to be moved down by one. |

---

## MOVE_MEMBER_UP Procedure

Adjusts the sequence ID of specified member in the given named collection up by one (add one), swapping sequence ID with the one it is replacing. For example, 2 becomes 3 and 3 becomes 2.

If a collection does not exist with the specified name for the current user in the same session and for the current application ID, an application error occurs.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

If the member specified by sequence ID `p_seq` is the highest sequence in the collection, an application error is not returned.

Syntax

```sql
APEX_COLLECTION.MOVE_MEMBER_UP (
    p_collection_name   IN VARCHAR2,
    p_seq               IN NUMBER )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. Maximum length is 255 bytes. Collection names are not case sensitive and are converted to upper case. An error is returned if this collection does not exist with the specified name of the current user in the same session. |
| `p_seq` | Identifies the sequence number of the collection member to be moved up by one. |

---

## RESEQUENCE_COLLECTION Procedure

For a named collection, updates the `seq_id` value of each member so that no gaps exist in the sequencing. For example, a collection with the following set of sequence IDs (1,2,3,5,8,9) becomes (1,2,3,4,5,6).

If a collection does not exist with the specified name for the current user in the same session and for the current application ID, an application error occurs.

Syntax

```sql
APEX_COLLECTION.RESEQUENCE_COLLECTION (
    p_collection_name   IN VARCHAR2);
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection to resequence. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |

---

## RESET_COLLECTION_CHANGED Procedure

Resets the collection changed flag (mark as not changed) for a given collection.

If a collection does not exist with the specified name for the current user in the same session and for the current application ID, an application error occurs.

Syntax

```sql
APEX_COLLECTION.RESET_COLLECTION_CHANGED (
    p_collection_name   IN VARCHAR2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection to reset the collection changed flag. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |

---

## RESET_COLLECTION_CHANGED_ALL Procedure

Resets the collection changed flag (mark as not changed) for all collections in the user's current session.

Syntax

```sql
APEX_COLLECTION.RESET_COLLECTION_CHANGED_ALL;
```

Parameters

None.

---

## SORT_MEMBERS Procedure

Reorders the members of a given collection by the column number specified by `p_sort_on_column_number`. This sorts the collection by a particular column or attribute in the collection and reassigns the sequence IDs of each number such that no gaps exist.

If a collection does not exist with the specified name for the current user in the same session and for the current application ID, an application error occurs.

Syntax

```sql
APEX_COLLECTION.SORT_MEMBERS (
    p_collection_name       IN VARCHAR2,
    p_sort_on_column_number IN NUMBER )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection to sort. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |
| `p_sort_on_column_number` | The column number used to sort the collection. The domain of possible values is 1 to 50. |

---

## TRUNCATE_COLLECTION Procedure

Removes all members from a named collection.

If a collection does not exist with the specified name for the current user in the same session and for the current application ID, an application error occurs.

Syntax

```sql
APEX_COLLECTION.TRUNCATE_COLLECTION (
    p_collection_name   IN VARCHAR2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection to truncate. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |

---

## UPDATE_MEMBER Procedure

Updates the specified member in the given named collection.

If a collection does not exist with the specified name for the current user in the same session and for the current application ID, an application error occurs.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

Note:

Using this procedure sets the columns identified and nullifies any columns not identified. To update specific columns, without affecting the values of other columns, use UPDATE_MEMBER_ATTRIBUTE Procedure Signature 1.

Syntax

```sql
APEX_COLLECTION.UPDATE_MEMBER (
    p_collection_name   IN VARCHAR2,
    p_seq               IN VARCHAR2 DEFAULT NULL,
    p_c001              IN VARCHAR2 DEFAULT NULL,
    p_c002              IN VARCHAR2 DEFAULT NULL,
    p_c003              IN VARCHAR2 DEFAULT NULL,
    …
    p_c050              IN VARCHAR  DEFAULT NULL,
    p_n001              IN NUMBER   DEFAULT NULL,
    p_n002              IN NUMBER   DEFAULT NULL,
    p_n003              IN NUMBER   DEFAULT NULL,
    p_n004              IN NUMBER   DEFAULT NULL,
    p_n005              IN NUMBER   DEFAULT NULL,
    p_d001              IN DATE     DEFAULT NULL,
    p_d002              IN DATE     DEFAULT NULL,
    p_d003              IN DATE     DEFAULT NULL,
    p_d004              IN DATE     DEFAULT NULL,
    p_d005              IN DATE     DEFAULT NULL,
    p_clob001           IN CLOB     DEFAULT empty_clob(),
    p_blob001           IN BLOB     DEFAULT empty-blob(),
    p_xmltype001        IN XMLTYPE  DEFAULT NULL )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. Also, the number of members added is based on the number of elements in the first array.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection to update. Maximum length is 255 bytes. Collection names are not case-sensitive and are converted to upper case. |
| `p_seq` | Identifies the sequence number of the collection member to be updated. |
| `p_c001`through `p_c050` | Attribute value of the member to be added. Maximum length is 4,000 bytes. Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. |
| `p_n001 through p_n005` | Attribute value of the numeric attributes to be added or updated. |
| `p_d001` through `p_d005` | Attribute value of the date attributes to be added or updated. |
| `p_clob001` | Use `p_clob001` for collection member attributes that exceed 4,000 characters. |
| `p_blob001` | Use `p_blob001` for binary collection member attributes. |
| `p_xmltype001` | Use `p_xmltype001` to store well-formed XML. |

---

## UPDATE_MEMBERS Procedure

Updates the array of members for the given named collection.

If a collection does not exist with the specified name for the current user in the same session and for the current application ID, an application error occurs.

The count of elements in the `p_seq` PL/SQL table is used as the total number of items across all PL/SQL tables. If `p_seq.count = 2` and `p_c001.count = 10`, only two members are updated.

If `p_seq` is NULL, an application error occurs.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

Syntax

```sql
APEX_COLLECTION.UPDATE_MEMBERS (
    p_collection_name IN VARCHAR2,
    p_seq             IN apex_application_global.vc_arr2 DEFAULT empty_vc_arr,
    p_c001            IN apex_application_global.vc_arr2 DEFAULT empty_vc_arr,
    p_c002            IN apex_application_global.vc_arr2 DEFAULT empty_vc_arr,
    p_c003            IN apex_application_global.vc_arr2 DEFAULT empty_vc_arr,
    ...
    p_c050            IN apex_application_global.vc_arr2 DEFAULT empty_vc_arr,
    p_n001            IN apex_application_global.n_arr   DEFAULT empty_n_arr,
    p_n002            IN apex_application_global.n_arr   DEFAULT empty_n_arr,
    p_n003            IN apex_application_global.n_arr   DEFAULT empty_n_arr,
    p_n004            IN apex_application_global.n_arr   DEFAULT empty_n_arr,
    p_n005            IN apex_application_global.n_arr   DEFAULT empty_n_arr,
    p_d001            IN apex_application_global.d_arr   DEFAULT empty_d_arr,
    p_d002            IN apex_application_global.d_arr   DEFAULT empty_d_arr,
    p_d003            IN apex_application_global.d_arr   DEFAULT empty_d_arr,
    p_d004            IN apex_application_global.d_arr   DEFAULT empty_d_arr,
    p_d005            IN apex_application_global.d_arr   DEFAULT empty_d_arr )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. Also, the number of members added is based on the number of elements in the first array.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection to update. Maximum length is 255 bytes. Collection names are not case-sensitive and are converted to upper case. |
| `p_seq` | Array of member sequence IDs to be updated. The count of the `p_seq` array is used across all arrays. |
| `p_c001 through p_c050` | Array of attribute values to be updated. |
| `p_n001 through p_n005` | Array of numeric attribute values to be updated. |
| `p_d001` through `p_d005` | Array of date attribute values to be updated. |

---

## UPDATE_MEMBER_ATTRIBUTE Procedure Signature 1

Updates the specified member attribute in the given named collection.

If a collection does not exist with the specified name for the current user in the same session for the current application ID, an application error occurs.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

If the attribute number specified is invalid or outside the range 1-50, an error occurs.

Any attribute value exceeding 4,000 bytes are truncated to 4,000 bytes.

Syntax

```sql
APEX_COLLECTION.UPDATE_MEMBER_ATTRIBUTE (
    p_collection_name   IN VARCHAR2,
    p_seq               IN NUMBER,
    p_attr_number       IN NUMBER,
    p_attr_value        IN VARCHAR2 )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. Also, the number of members added is based on the number of elements in the first array.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. Maximum length is 255 bytes. Collection names are case-insensitive and are converted to upper case. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |
| `p_seq` | Sequence ID of the collection member to be updated. |
| `p_attr_number` | Attribute number of the member attribute to be updated. Valid values are 1 through 50. Any number outside of this range is ignored. |
| `p_attr_value` | Attribute value of the member attribute to be updated. |

---

## UPDATE_MEMBER_ATTRIBUTE Procedure Signature 2

Updates the specified CLOB member attribute in the given named collection.

If a collection does not exist with the specified name for the current user in the same session for the current application ID, an application error occurs.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

If the attribute number specified is invalid or outside the valid range (currently only 1 for CLOB), an error occurs.

Syntax

```sql
APEX_COLLECTION.UPDATE_MEMBER_ATTRIBUTE (
    p_collection_name   IN VARCHAR2,
    p_seq               IN NUMBER,
    p_clob_number       IN NUMBER,
    p_clob_value        IN CLOB )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. Also, the number of members added is based on the number of elements in the first array.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. Maximum length can be 255 bytes. Collection names are case-insensitive and are converted to upper case. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |
| `p_seq` | Sequence ID of the collection member to be updated. |
| `p_clob_number` | Attribute number of the CLOB member attribute to be updated. Valid value is 1. Any number outside of this range is ignored. |
| `p_clob_value` | Attribute value of the CLOB member attribute to be updated. |

---

## UPDATE_MEMBER_ATTRIBUTE Procedure Signature 3

Updates the specified BLOB member attribute in the given named collection.

If a collection does not exist with the specified name for the current user in the same session for the current application ID, an application error occurs.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

If the attribute number specified is invalid or outside the valid range (currently only 1 for BLOB), an error occurs.

Syntax

```sql
APEX_COLLECTION.UPDATE_MEMBER_ATTRIBUTE (
    p_collection_name   IN VARCHAR2,
    p_seq               IN NUMBER,
    p_blob_number       IN NUMBER,
    p_blob_value        IN BLOB )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. Also, the number of members added is based on the number of elements in the first array.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. Maximum length is 255 bytes. Collection names are case-insensitive and are converted to upper case. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |
| `p_seq` | Sequence ID of the collection member to be updated. |
| `p_blob_number` | Attribute number of the BLOB member attribute to be updated. Valid value is 1. Any number outside of this range is ignored. |
| `p_blob_value` | Attribute value of the BLOB member attribute to be updated. |

---

## UPDATE_MEMBER_ATTRIBUTE Procedure Signature 4

Updates the specified XMLTYPE member attribute in the given named collection.

If a collection does not exist with the specified name for the current user in the same session for the current application ID, an application error occurs.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

If the attribute number specified is invalid or outside the valid range (currently only 1 for XMLTYPE), an error occurs.

Syntax

```sql
APEX_COLLECTION.UPDATE_MEMBER_ATTRIBUTE (
    p_collection_name   IN VARCHAR2,
    p_seq               IN NUMBER,
    p_xmltype_number    IN NUMBER,
    p_xmltype_value     IN SYS.XMLTYPE )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. Also, the number of members added is based on the number of elements in the first array.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. Maximum length can be 255 bytes. Collection names are case-insensitive and are converted to upper case. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |
| `p_seq` | Sequence ID of the collection member to be updated. |
| `p_xmltype_number` | Attribute number of the XMLTYPE member attribute to be updated. Valid value is 1. Any number outside of this range is ignored. |
| `p_xmltype_value` | Attribute value of the XMLTYPE member attribute to be updated. |

---

## UPDATE_MEMBER_ATTRIBUTE Procedure Signature 5

Updates the specified `NUMBER` member attribute in the given named collection.

If a collection does not exist with the specified name for the current user in the same session for the current application ID, an application error occurs.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

If the attribute number specified is invalid or outside the valid range (currently only 1 through 5 for `NUMBER`), an error occurs.

Syntax

```sql
APEX_COLLECTION.UPDATE_MEMBER_ATTRIBUTE (
    p_collection_name IN VARCHAR2,
    p_seq             IN NUMBER,
    p_attr_number     IN NUMBER,
    p_number_value    IN NUMBER )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. The number of members added is based on the number of elements in the first array.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. Maximum length can be 255 bytes. Collection names are case-insensitive and are converted to upper case. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |
| `p_seq` | Sequence ID of the collection member to be updated. |
| `p_attr_number` | Attribute number of the `NUMBER` member attribute to be updated. Valid value is 1 through 5. Any number outside of this range is ignored. |
| `p_number_value` | Attribute value of the NUMBER member attribute to be updated. |

---

## UPDATE_MEMBER_ATTRIBUTE Procedure Signature 6

Updates the specified `DATE` member attribute in the given named collection.

If a collection does not exist with the specified name for the current user in the same session for the current application ID, an application error occurs.

If the member specified by sequence ID `p_seq` does not exist, an application error occurs.

If the attribute number specified is invalid or outside the valid range (currently only 1 through 5 for `DATE`), an error occurs.

Syntax

```sql
APEX_COLLECTION.UPDATE_MEMBER_ATTRIBUTE (
    p_collection_name   IN VARCHAR2,
    p_seq               IN NUMBER,
    p_attr_number       IN NUMBER,
    p_date_value        IN DATE )
```

Parameters

Note:

Any character attribute exceeding 4,000 characters is truncated to 4,000 characters. Also, the number of members added is based on the number of elements in the first array.

| Parameter | Description |
| --- | --- |
| `p_collection_name` | The name of the collection. Maximum length can be 255 bytes. Collection names are case-insensitive and are converted to upper case. An error is returned if this collection does not exist with the specified name of the current user and in the same session. |
| `p_seq` | Sequence ID of the collection member to be updated. |
| `p_attr_number` | Attribute number of the `DATE` member attribute to be updated. Valid value is 1 through 5. Any number outside of this range is ignored. |
| `p_date_value` | Attribute value of the `DATE` member attribute to be updated. |