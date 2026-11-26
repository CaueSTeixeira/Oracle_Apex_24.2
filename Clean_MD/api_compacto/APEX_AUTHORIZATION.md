<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_AUTHORIZATION (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_AUTHORIZATION

The `APEX_AUTHORIZATION` package contains public utility functions used for controlling and querying access rights to the application.

---

## ENABLE_DYNAMIC_GROUPS Procedure

This procedure enables groups in the current session. These groups do not have to be created in the Oracle APEX workspace repository, but can be loaded from an LDAP repository or retrieved from a trusted HTTP header. Enabling a group that exists in the workspace repository and has other groups granted to it, also enables the granted groups.

If Real Application Security, available with Oracle
Database Release 12g, is enabled for the authentication scheme, all dynamic groups are enabled as RAS dynamic or external groups (depending whether the group exists in `dba_xs_dynamic_roles`).

This procedure must be called during or immediately after authentication, for example, in a post-authentication procedure.

Syntax

```sql
APEX_AUTHORIZATION.ENABLE_DYNAMIC_GROUPS (
    p_group_names   IN apex_t_varchar2 )
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_group_names` | Table of group names. |

---

## IS_AUTHORIZED Function

This function determines if the current user passes the authorization with name `p_authorization_name`. For performance reasons, authorization results are cached. Because of this, the function may not always evaluate the authorization when called, but take the result out of the cache.

See Also:

Changing the Evaluation Point Attribute in Oracle APEX App Builder
User’s Guide

Syntax

```sql
APEX_AUTHORIZATION.IS_AUTHORIZED (
    p_authorization_name IN VARCHAR2 )
    RETURN BOOLEAN;
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_authorization_name` | The name of an authorization scheme in the application. |

Returns

| Parameter | Description |
| --- | --- |
| `TRUE` | If the authorization is successful. |
| `FALSE` | If the authorization is not successful. |

---

## RESET_CACHE Procedure

This procedure resets the authorization caches for the session and forces a re-evaluation when an authorization is checked next.

Syntax

```sql
APEX_AUTHORIZATION.RESET_CACHE;
```

Parameters

None.