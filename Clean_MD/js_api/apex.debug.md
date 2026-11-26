<!-- Fonte: JavaScript API Reference 24.2, aexjs/apex.debug.html -->

# Namespace: debug

## QuickNav

### Properties

* LOG_LEVEL

### Functions

* error
* getLevel
* info
* log
* message
* setLevel
* trace
* warn

## apex.debug

This namespace stores all debug functions of Oracle APEX.

### Properties

#### (static) LOG_LEVEL :object

Log level constants

##### Type:

* object

##### Properties:

| Name | Type | Description |
| --- | --- | --- |
| `OFF` | number | Logging is off. Value is 0. |
| `ERROR` | number | Error logging level. Value is 1. |
| `WARN` | number | Warning logging level. Value is 2. |
| `INFO` | number | Information logging level. Value is 4. |
| `APP_TRACE` | number | Application tracing logging level. Value is 6. |
| `ENGINE_TRACE` | number | Engine tracing logging level. Value is 9. |

### Functions

#### (static) error(…arguments)

Log an error message. The error function always writes the error, regardless of the log level from the server
or set with apex.debug.setLevel.
Messages are written using the browsers built-in console logging, if available. If supported, console.trace is called.
Older browsers may not support the console object or all of its features.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `arguments` | \* | <repeatable> | Any number of parameters which will be logged to the console. |

This example writes the message "Update Failed" to the console.

This example writes an exception message (from variable
`ex`) to the console.

#### (static) getLevel() → {number}

Method that returns the debug log level.
The debug log level is synchronized with hidden input element `#pdebug`.
In a developer session, the default log level is WARN.

##### Returns:

Logging level as an integer 1 to 9, or 0 to indicate debug logging is turned off.

Type
:   number

This example retrieves the logging level, prepends "Level=" and logs to the console.

#### (static) info(…arguments)

Log an informational message. Similar to apex.debug.message with the level set to INFO.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `arguments` | \* | <repeatable> | Any number of parameters which will be logged to the console. |

This example prints an informational message to the console if the log level is
INFO or greater.

#### (static) log(…arguments)

Log a message. Similar to apex.debug.message with the level set to the highest level.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `arguments` | \* | <repeatable> | Any number of parameters which will be logged to the console. |

This example gets the logging level and writes it to the console,
regardless of the current logging level.

#### (static) message(pLevel, …arguments)

Log a message at the given debug log level. The log level set from the server or with apex.debug.setLevel
controls if the message is actually written. If the set log level is >= pLevel then the message is written.
Messages are written using the browsers built-in console logging, if available.
Older browsers may not support the console object or all of its features.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pLevel` | number |  | A number from 1 to 9, where level 1 is most important, and level 9 is least important. Can be one of the apex.debug.LOG_LEVEL constants. Any other value such as 0 will turn off debug logging. |
| `arguments` | \* | <repeatable> | Any number of parameters which will be logged to the console. |

This example writes the message "Testing" to the console if the logging level is
greater than or equal to 7.

#### (static) setLevel(pLevel)

Method that sets the debug log level. Log messages at or below the specified level are written to the
console log. It is rarely necessary to call this function because the debug log level is
synchronized with the hidden input element `#pdebug` that comes from the server.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pLevel` | number | A number from 1 to 9, where level 1 is most important, and level 9 is least important. Can be one of the LOG_LEVEL constants. Any other value such as 0 will turn off debug logging. |

This example sets the logging level to application tracing.

#### (static) trace(…arguments)

Log a trace message. Similar to apex.debug.message with the level set to APP_TRACE.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `arguments` | \* | <repeatable> | Any number of parameters which will be logged to the console. |

This example writes a log message to the console if the debug log level is APP_TRACE
or greater.

#### (static) warn(…arguments)

Log a warning message. Similar to apex.debug.message with the level set to WARN.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `arguments` | \* | <repeatable> | Any number of parameters which will be logged to the console. |

This example writes a warning message to the console if the debug log level is WARN or greater.

Documentation generated by JSDoc 4.0.3 on Wed Nov 27 2024 04:42:15 GMT+0000 (Coordinated Universal Time)

Oracle APEX Release 24.2, JavaScript API Reference

Copyright © 2003, 2025, Oracle and/or its affiliates. All rights reserved.