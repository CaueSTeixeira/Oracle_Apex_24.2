# Índice de pacotes APEX_* (24.2) — nomes dos subprogramas
Fonte: https://docs.oracle.com/en/database/oracle/apex/24.2/aeapi/

## APEX_UTIL
The APEX_UTIL package provides utilities you can use when programming in the Oracle APEX environment. You can use the APEX_UTIL package to get and set session state, to get files, to check authorizations for users, to reset different states for users, to get and purge cache information, and to get and set preferences for users.

- BLOB_TO_CLOB Function
- CACHE_GET_DATE_OF_PAGE_CACHE Function
- CACHE_GET_DATE_OF_REGION_CACHE Function
- CACHE_PURGE_BY_APPLICATION Procedure
- CACHE_PURGE_BY_PAGE Procedure
- CACHE_PURGE_STALE Procedure
- CHANGE_CURRENT_USER_PW Procedure
- CHANGE_PASSWORD_ON_FIRST_USE Function
- CLOB_TO_BLOB Function
- CLOSE_OPEN_DB_LINKS Procedure
- CLEAR_APP_CACHE Procedure
- CLEAR_PAGE_CACHE Procedure
- CLEAR_USER_CACHE Procedure
- COUNT_CLICK Procedure
- CREATE_USER Procedure
- CREATE_USER_GROUP Procedure
- CURRENT_USER_IN_GROUP Function
- CUSTOM_CALENDAR Procedure (Deprecated)
- DELETE_FEEDBACK Procedure
- DELETE_FEEDBACK_ATTACHMENT Procedure
- DELETE_USER_GROUP Procedure Signature 1
- DELETE_USER_GROUP Procedure Signature 2
- DOWNLOAD_PRINT_DOCUMENT Procedure Signature 1
- DOWNLOAD_PRINT_DOCUMENT Procedure Signature 2
- DOWNLOAD_PRINT_DOCUMENT Procedure Signature 3
- DOWNLOAD_PRINT_DOCUMENT Procedure Signature 4
- EDIT_USER Procedure
- END_USER_ACCOUNT_DAYS_LEFT Function
- EXPIRE_END_USER_ACCOUNT Procedure
- EXPIRE_WORKSPACE_ACCOUNT Procedure
- EXPORT_USERS Procedure
- FEEDBACK_ENABLED Function
- FETCH_APP_ITEM Function
- FETCH_USER Procedure Signature 1
- FETCH_USER Procedure Signature 2
- FETCH_USER Procedure Signature 3
- FIND_SECURITY_GROUP_ID Function
- FIND_WORKSPACE Function
- GET_ACCOUNT_LOCKED_STATUS Function
- GET_APEX_OWNER Function
- GET_APPLICATION_STATUS Function (Deprecated)
- GET_ATTRIBUTE Function
- GET_AUTHENTICATION_RESULT Function
- GET_BLOB_FILE_SRC Function
- GET_BUILD_OPTION_STATUS Function Signature 1 (Deprecated)
- GET_BUILD_OPTION_STATUS Function Signature 2 (Deprecated)
- GET_CURRENT_USER_ID Function
- GET_DEFAULT_SCHEMA Function
- GET_EDITION Function
- GET_EMAIL Function
- GET_FEEDBACK_FOLLOW_UP Function
- GET_FILE Procedure
- GET_FILE_ID Function
- GET_FIRST_NAME Function
- GET_GLOBAL_NOTIFICATION Function (Deprecated)
- GET_GROUPS_USER_BELONGS_TO Function
- GET_GROUP_ID Function
- GET_GROUP_NAME Function
- GET_HASH Function
- GET_HIGH_CONTRAST_MODE_TOGGLE Function
- GET_LAST_NAME Function
- GET_NUMERIC_SESSION_STATE Function
- GET_PREFERENCE Function
- GET_PRINT_DOCUMENT Function Signature 1
- GET_PRINT_DOCUMENT Function Signature 2
- GET_PRINT_DOCUMENT Function Signature 3
- GET_PRINT_DOCUMENT Function Signature 4
- GET_SCREEN_READER_MODE_TOGGLE Function
- GET_SESSION_LANG Function
- GET_SESSION_STATE Function
- GET_SESSION_TERRITORY Function
- GET_SESSION_TIME_ZONE Function
- GET_SINCE Function Signature 1
- GET_SINCE Function Signature 2
- GET_SUPPORTING_OBJECT_SCRIPT Function
- GET_SUPPORTING_OBJECT_SCRIPT Procedure
- GET_USER_ID Function
- GET_USER_ROLES Function
- GET_USERNAME Function
- HOST_URL Function
- HTML_PCT_GRAPH_MASK Function
- INCREMENT_CALENDAR Procedure (Deprecated)
- IR_CLEAR Procedure (Deprecated)
- IR_DELETE_REPORT Procedure (Deprecated)
- IR_DELETE_SUBSCRIPTION Procedure (Deprecated)
- IR_FILTER Procedure (Deprecated)
- IR_RESET Procedure (Deprecated)
- IS_HIGH_CONTRAST_SESSION Function
- IS_HIGH_CONTRAST_SESSION_YN Function
- IS_LOGIN_PASSWORD_VALID Function
- IS_SCREEN_READER_SESSION Function
- IS_SCREEN_READER_SESSION_YN Function
- IS_USERNAME_UNIQUE Function
- KEYVAL_NUM Function
- KEYVAL_VC2 Function
- LOCK_ACCOUNT Procedure
- PASSWORD_FIRST_USE_OCCURRED Function
- PREPARE_URL Function
- PRN Procedure
- PUBLIC_CHECK_AUTHORIZATION Function (Deprecated)
- PURGE_REGIONS_BY_APP Procedure
- PURGE_REGIONS_BY_NAME Procedure
- PURGE_REGIONS_BY_PAGE Procedure
- REDIRECT_URL Procedure
- REMOVE_PREFERENCE Procedure
- REMOVE_SORT_PREFERENCES Procedure
- REMOVE_USER Procedure Signature 1
- REMOVE_USER Procedure Signature 2
- REPLY_TO_FEEDBACK Procedure
- RESET_AUTHORIZATIONS Procedure (Deprecated)
- RESET_PASSWORD Procedure
- RESET_PW Procedure
- SAVEKEY_NUM Function
- SAVEKEY_VC2 Function
- SET_APP_BUILD_STATUS Procedure (Deprecated)
- SET_APPLICATION_STATUS Procedure (Deprecated)
- SET_ATTRIBUTE Procedure
- SET_AUTHENTICATION_RESULT Procedure
- SET_BUILD_OPTION_STATUS Procedure (Deprecated)
- SET_CURRENT_THEME_STYLE Procedure (Deprecated)
- SET_CUSTOM_AUTH_STATUS Procedure
- SET_EDITION Procedure
- SET_EMAIL Procedure
- SET_FIRST_NAME Procedure
- SET_GLOBAL_NOTIFICATION Procedure (Deprecated)
- SET_GROUP_GROUP_GRANTS Procedure
- SET_GROUP_USER_GRANTS Procedure
- SET_LAST_NAME Procedure
- SET_PARSING_SCHEMA_FOR _REQUEST Procedure
- SET_PREFERENCE Procedure
- SET_SECURITY_GROUP_ID Procedure
- SET_SESSION_HIGH_CONTRAST_OFF Procedure
- SET_SESSION_HIGH_CONTRAST_ON Procedure
- SET_SESSION_LANG Procedure
- SET_SESSION_LIFETIME_SECONDS Procedure
- SET_SESSION_MAX_IDLE_SECONDS Procedure
- SET_SESSION_SCREEN_READER_OFF Procedure
- SET_SESSION_SCREEN_READER_ON Procedure
- SET_SESSION_STATE Procedure
- SET_SESSION_TERRITORY Procedure
- SET_SESSION_TIME_ZONE Procedure
- SET_USERNAME Procedure
- SET_WORKSPACE Procedure
- SHOW_HIGH_CONTRAST_MODE_TOGGLE Procedure
- SHOW_SCREEN_READER_MODE_TOGGLE Procedure
- STRING_TO_TABLE Function (Deprecated)
- STRONG_PASSWORD_CHECK Procedure
- STRONG_PASSWORD_VALIDATION Function
- SUBMIT_FEEDBACK Procedure
- SUBMIT_FEEDBACK_FOLLOWUP Procedure
- TABLE_TO_STRING Function (Deprecated)
- UNEXPIRE_END_USER_ACCOUNT Procedure
- UNEXPIRE_WORKSPACE_ACCOUNT Procedure
- UNLOCK_ACCOUNT Procedure
- URL_ENCODE Function (Deprecated)
- WORKSPACE_ACCOUNT_DAYS_LEFT Function

## APEX_APPLICATION
The APEX_APPLICATION package is a PL/SQL package that implements the Oracle APEX rendering engine. You can use this package to take advantage of many global variables.

- Working with G_Fnn Arrays (Legacy)
- Global Variables
- HELP Procedure
- STOP_APEX_ENGINE Procedure

## APEX_ERROR
The APEX_ERROR package provides the interface declarations and utility functions for an error handling function and includes procedures and functions to raise errors in an APEX application.

- Constants and Attributes Used for Result Types
- Example of an Error Handling Function
- ADD_ERROR Procedure Signature 1
- ADD_ERROR Procedure Signature 2
- ADD_ERROR Procedure Signature 3
- ADD_ERROR Procedure Signature 4
- ADD_ERROR Procedure Signature 5
- AUTO_SET_ASSOCIATED_ITEM Procedure
- EXTRACT_CONSTRAINT_NAME Function
- GET_FIRST_ORA_ERROR_TEXT Function
- HAVE_ERRORS_OCCURRED Function
- INIT_ERROR_RESULT Function

## APEX_DEBUG
The APEX_DEBUG package provides utility functions for managing the debug message log. Specifically, this package provides the necessary APIs to instrument and debug PL/SQL code contained within your Oracle APEX application as well as PL/SQL code in database stored procedures and functions. Instrumenting your PL/SQL code makes it much easier to track down bugs and isolate unexpected behavior more quickly.

- Constants
- DISABLE Procedure
- DISABLE_DBMS_OUTPUT Procedure
- ENABLE Procedure
- ENTER Procedure
- ENABLE_DBMS_OUTPUT Procedure
- ERROR Procedure
- GET_LAST_MESSAGE_ID Function
- GET_PAGE_VIEW_ID Function
- INFO Procedure
- LOG_DBMS_OUTPUT Procedure
- LOG_LONG_MESSAGE Procedure
- LOG_MESSAGE Procedure (Deprecated)
- LOG_PAGE_SESSION_STATE Procedure
- MESSAGE Procedure
- REMOVE_DEBUG_BY_AGE Procedure
- REMOVE_DEBUG_BY_APP Procedure
- REMOVE_DEBUG_BY_VIEW Procedure
- REMOVE_SESSION_MESSAGES Procedure
- TOCHAR Function
- TRACE Procedure
- WARN Procedure
- Accessing Debugging Mode

## APEX_COLLECTION
Collections enable you to temporarily capture one or more nonscalar values. You can use collections to store rows and columns currently in session state so they can be accessed, manipulated, or processed during a user's specific session. You can think of a collection as a bucket in which you temporarily store and name rows of information.

- About the APEX_COLLECTION API
- ADD_MEMBER Procedure
- ADD_MEMBER Function
- ADD_MEMBERS Procedure
- COLLECTION_EXISTS Function
- COLLECTION_HAS_CHANGED Function
- COLLECTION_MEMBER_COUNT Function
- CREATE_COLLECTION Procedure
- CREATE_COLLECTION_FROM_QUERY Procedure
- CREATE_COLLECTION_FROM_QUERY2 Procedure
- CREATE_COLLECTION_FROM_QUERY_B Procedure
- CREATE_COLLECTION_FROM_QUERY_B Procedure (No bind version)
- CREATE_COLLECTION_FROM_QUERYB2 Procedure
- CREATE_COLLECTION_FROM_QUERYB2 Procedure (No bind version)
- CREATE_OR_TRUNCATE_COLLECTION Procedure
- DELETE_ALL_COLLECTIONS Procedure
- DELETE_ALL_COLLECTIONS_SESSION Procedure
- DELETE_COLLECTION Procedure
- DELETE_MEMBER Procedure
- DELETE_MEMBERS Procedure
- GET_MEMBER_MD5 Function
- MERGE_MEMBERS Procedure
- MOVE_MEMBER_DOWN Procedure
- MOVE_MEMBER_UP Procedure
- RESEQUENCE_COLLECTION Procedure
- RESET_COLLECTION_CHANGED Procedure
- RESET_COLLECTION_CHANGED_ALL Procedure
- SORT_MEMBERS Procedure
- TRUNCATE_COLLECTION Procedure
- UPDATE_MEMBER Procedure
- UPDATE_MEMBERS Procedure
- UPDATE_MEMBER_ATTRIBUTE Procedure Signature 1
- UPDATE_MEMBER_ATTRIBUTE Procedure Signature 2
- UPDATE_MEMBER_ATTRIBUTE Procedure Signature 3
- UPDATE_MEMBER_ATTRIBUTE Procedure Signature 4
- UPDATE_MEMBER_ATTRIBUTE Procedure Signature 5
- UPDATE_MEMBER_ATTRIBUTE Procedure Signature 6

## APEX_SESSION
The APEX_SESSION package enables you to configure Oracle APEX sessions.

- ATTACH Procedure
- CREATE_SESSION Procedure
- DETACH Procedure
- DELETE_SESSION Procedure
- SET_DEBUG Procedure
- SET_TENANT_ID Procedure
- SET_TRACE Procedure

## APEX_SESSION_STATE
The APEX_SESSION_STATE package encapsulates utilities needed to read and assign session state values.

- Global Constants
- Data Types
- GET_CLOB Function
- GET_NUMBER Function
- GET_TIMESTAMP Function
- GET_VALUE Function
- GET_VARCHAR2 Function
- SET_VALUE Procedure Signature 1
- SET_VALUE Procedure Signature 2
- SET_VALUE Procedure Signature 3

## APEX_STRING
Unless otherwise noted, the APIs expect arrays to be continuous (that is, without holes that coll.delete(n) operations generate).

- FORMAT Function
- GET_INITIALS Function
- GET_SEARCHABLE_PHRASES Function
- GREP Function Signature 1
- GREP Function Signature 2
- GREP Function Signature 3
- INDEX_OF Function Signature 1
- INDEX_OF Function Signature 2
- JOIN_CLOB Function
- JOIN_CLOBS Function
- JOIN Function Signature 1
- JOIN Function Signature 2
- NEXT_CHUNK Function
- PLIST_DELETE Procedure
- PLIST_EXISTS Function
- PLIST_GET Function
- PLIST_GET_KEY Function
- PLIST_PUSH Procedure
- PLIST_PUT Function
- PLIST_TO_JSON_CLOB Function
- PUSH Procedure Signature 1
- PUSH Procedure Signature 2
- PUSH Procedure Signature 3
- PUSH Procedure Signature 4
- PUSH Procedure Signature 5
- PUSH Procedure Signature 6
- PUSH Procedure Signature 7
- SHUFFLE Function
- SHUFFLE Procedure
- SPLIT Function Signature 1
- SPLIT Function Signature 2
- SPLIT_CLOBS Function
- SPLIT_NUMBERS Function
- STRING_TO_TABLE Function
- TABLE_TO_CLOB Function
- TABLE_TO_STRING Function

## APEX_JSON
This package includes utilities that parse and generate JSON.

- APEX_JSON Overview and Examples
- Constants and Data Types
- CLOSE_ALL Procedure
- CLOSE_ARRAY Procedure
- CLOSE_OBJECT Procedure
- DOES_EXIST Function
- FIND_PATHS_LIKE Function
- FLUSH Procedure
- FREE_OUTPUT Procedure
- GET_BOOLEAN Function
- GET_CLOB Function
- GET_CLOB_OUTPUT Function
- GET_COUNT Function
- GET_DATE Function
- GET_MEMBERS Function
- GET_NUMBER Function
- GET_SDO_GEOMETRY Function
- GET_T_NUMBER Function
- GET_T_VARCHAR2 Function
- GET_VALUE Function
- GET_VALUE_KIND Function
- GET_VARCHAR2 Function
- INITIALIZE_CLOB_OUTPUT Procedure
- INITIALIZE_OUTPUT Procedure
- OPEN_ARRAY Procedure
- OPEN_OBJECT Procedure
- PARSE Procedure Signature 1
- PARSE Procedure Signature 2
- STRINGIFY Function Signature 1
- STRINGIFY Function Signature 2
- STRINGIFY Function Signature 3
- STRINGIFY Function Signature 4
- STRINGIFY Function Signature 5
- TO_MEMBER_NAME Function
- TO_XMLTYPE Function
- TO_XMLTYPE_SQL Function
- WRITE Procedure Signature 1
- WRITE Procedure Signature 2
- WRITE Procedure Signature 3
- WRITE Procedure Signature 4
- WRITE Procedure Signature 5
- WRITE Procedure Signature 6
- WRITE Procedure Signature 7
- WRITE Procedure Signature 8
- WRITE Procedure Signature 9
- WRITE Procedure Signature 10
- WRITE Procedure Signature 11
- WRITE Procedure Signature 12
- WRITE Procedure Signature 13
- WRITE Procedure Signature 14
- WRITE Procedure Signature 15
- WRITE Procedure Signature 16
- WRITE Procedure Signature 17
- WRITE Procedure Signature 18
- WRITE Procedure Signature 19
- WRITE Procedure Signature 20
- WRITE Procedure Signature 21
- WRITE_CONTEXT Procedure

## APEX_PAGE
The APEX_PAGE package is the public API for handling pages.

- Global Constants
- GET_PAGE_MODE Function
- GET_UI_TYPE Function (Deprecated)
- GET_URL Function
- IS_DESKTOP_UI Function (Deprecated)
- IS_READ_ONLY Function
- PURGE_CACHE Procedure

## APEX_AUTHORIZATION
The APEX_AUTHORIZATION package contains public utility functions used for controlling and querying access rights to the application.

- ENABLE_DYNAMIC_GROUPS Procedure
- IS_AUTHORIZED Function
- RESET_CACHE Procedure

## APEX_ITEM
This API is designated as legacy.

- CHECKBOX2 Function
- DATE_POPUP Function
- DATE_POPUP2 Function
- DISPLAY_AND_SAVE Function
- HIDDEN Function
- MD5_CHECKSUM Function
- MD5_HIDDEN Function
- POPUP_FROM_LOV Function
- POPUP_FROM_QUERY Function
- POPUPKEY_FROM_LOV Function
- POPUPKEY_FROM_QUERY Function
- RADIOGROUP Function
- SELECT_LIST Function
- SELECT_LIST_FROM_LOV Function
- SELECT_LIST_FROM_LOV_XL Function
- SELECT_LIST_FROM_QUERY Function
- SELECT_LIST_FROM_QUERY_XL Function
- SWITCH Function
- TEXT Function
- TEXTAREA Function
- TEXT_FROM_LOV Function
- TEXT_FROM_LOV_QUERY Function