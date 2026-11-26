<!-- Fonte: Oracle APEX 24.2 API Reference, pacote APEX_SESSION (docs.oracle.com/en/database/oracle/apex/24.2/aeapi/) -->

## APEX_SESSION

The APEX_SESSION package enables you to configure Oracle APEX sessions.

---

## ATTACH Procedure

This procedure sets the environment and runs the Initialization PL/SQL Code based on the given application and current session.

Syntax

```sql
APEX_SESSION.ATTACH (
    p_app_id        IN  NUMBER,
    p_page_id       IN  NUMBER,
    p_session_id    IN  NUMBER );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_app_id` | The application ID. |
| `p_page_id` | The application page. |
| `p_session_id` | The session ID. |

Raises

* `WWV_FLOW.APP_NOT_FOUND_ERR`: Application does not exist or caller has no access to the workspace.
* `APEX.SESSION.EXPIRED`: Your session has ended.
* `SECURITY_GROUP_ID_INVALID`: Security Group ID (your workspace identity) is invalid.

---

## CREATE_SESSION Procedure

This procedure creates a new session for the given application, sets the environment, and runs the application's Initialization PL/SQL Code.

Syntax

```sql
APEX_SESSION.CREATE_SESSION (
   p_app_id                   IN NUMBER,
   p_page_id                  IN NUMBER,
   p_username                 IN VARCHAR2,
   p_call_post_authentication IN BOOLEAN DEFAULT FALSE );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_app_id` | The application id. |
| `p_page_id` | The application page. |
| `p_username` | The session user. |
| `p_call_post_authentication` | If true, call post-authentication procedure. The default is false. |

Raises

`WWV_FLOW.APP_NOT_FOUND_ERR`: The application does not exist or the caller has no access to the workspace.

---

## DETACH Procedure

This procedure detaches from the current session, resets the environment and runs the application's Cleanup PL/SQL Code. This procedure does nothing if no session is attached.

Syntax

```sql
APEX_SESSION.DETACH;
```

---

## DELETE_SESSION Procedure

This procedure deletes the session with the given ID. If the session is currently
attached, call the application's Cleanup PL/SQL Code and reset the environment.

Syntax

```sql
APEX_SESSION.DELETE_SESSION (
    p_session_id    IN  NUMBER  DEFAULT apex_application.g_instance );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_session_id` | The session ID. |

Raises

* `APEX.SESSION.EXPIRED`: Your session has ended.
* `SECURITY_GROUP_ID_INVALID`: Security Group ID (your workspace identity) is invalid.

---

## SET_DEBUG Procedure

This procedure sets debug level for all future requests in a session.

Syntax

```sql
APEX_SESSION.SET_DEBUG (
    p_session_id    IN NUMBER DEFAULT apex_application.g_instance,
    p_level         IN apex_debug.t_log_level );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_session_id` | The session ID.  Note: The session must belong to the current workspace or the caller must be able to set the session's workspace. |
| `p_level` | The debug level. NULL disables debug, 1-9 sets a debug level. |

---

## SET_TENANT_ID Procedure

This procedure is used to associate a session with a tenant ID which can be used for building multitenant Oracle APEX applications. Once set, the value of the current tenant can be retrieved using the built-in `APP_TENANT_ID`.

Syntax

```sql
APEX_SESSION.SET_TENANT_ID (
    p_tenant_id IN VARCHAR2 );
```

Parameters

| Parameter | Description |
| --- | --- |
| `p_tenant_id` | The tenant ID to associate with a session |

Raises

`PE.DISPLAY_GROUP.SESSION_NOT_VALID`: The session doesn't exist.

`WWV_FLOW_SESSION_API.TENANT_ID_EXISTS`: The tenant ID has already been set.

---

## SET_TRACE Procedure

This procedure sets trace mode in all future requests of a session.

Syntax

```sql
APEX_SESSION.SET_TRACE (
    p_session_id    IN NUMBER  DEFAULT apex_application.g_instance,
    p_mode          IN VARCHAR2 );
```

Parameters

| Parameters | Description |
| --- | --- |
| `p_session_id` | The session ID.  The session must belong to the current workspace or the caller must be able to set the session's workspace. |
| `p_level` | The trace mode. NULL disables trace, SQL enables SQL trace. |