<!-- Fonte: JavaScript API Reference 24.2, aexjs/apex.lang.html -->

# Namespace: lang

## QuickNav

### Functions

* addMessages
* clearMessages
* format
* formatMessage
* formatMessageNoEscape
* formatNoEscape
* getMessage
* hasMessage
* loadMessages
* loadMessagesIfNeeded

## apex.lang

This namespace is used for text and message localization related functions of Oracle APEX.

### Functions

#### (static) addMessages(pMessages)

Add messages for use by apex.lang.getMessage and the format functions. Can be called multiple times.
Additional messages are merged. It is generally not necessary to call this function, because it is
automatically called with all the application text messages that have attribute *Used in JavaScript* set to on.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pMessages` | Object | An object whose properties are message keys (names), and the values are localized message text. |

This example adds a message with key "APPLY_BUTTON_LABEL" and message text "Apply".

#### (static) clearMessages()

Remove all messages. This method is rarely needed. Many Oracle APEX components rely on client-side
messages, so if you clear the messages you need to add any needed messages again.

This example removes all messages.

#### (static) format(pPattern, …pValues) → {string}

Formats a message.
Same as apex.lang.formatMessage except the message pattern is given directly.
It is already localized or isn't supposed to be.
It is not a key. The replacement arguments are HTML escaped.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pPattern` | string |  | The message pattern. |
| `pValues` | \* | <repeatable> | Any number of replacement values, one for each message parameter %0 to %9. Non string arguments are converted to strings. |

##### Returns:

The formatted message text.

Type
:   string

This example returns "Total cost: $34.00" assuming the orderTotal variable equals "34.00".

#### (static) formatMessage(pKey, …pValues) → {string}

Format a message. Parameters in the message, %0 to %9, are replaced with the corresponding function argument.
Use %% to include a single %. The replacement arguments are HTML escaped.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pKey` | string |  | The message key. The key is used to lookup the localized message text as if with getMessage. |
| `pValues` | \* | <repeatable> | Any number of replacement values, one for each message parameter %0 to %9. Non string arguments are converted to strings. |

##### Returns:

The localized and formatted message text. If the key is not found then the key is returned.

Type
:   string

This example returns "Process 60% complete" when the PROCESS_STATUS message text is
"Process %0%% complete" and the progress variable value is 60.

#### (static) formatMessageNoEscape(pKey, …pValues) → {string}

Same as apex.lang.formatMessage except the replacement arguments are not HTML escaped.
They must be known to be safe or will be used in a context that is safe.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pKey` | string |  | The message key. The key is used to lookup the localized message text as if with getMessage. |
| `pValues` | \* | <repeatable> | Any number of replacement values, one for each message parameter %0 to %9. Non string arguments are converted to strings. |

##### Returns:

The localized and formatted message text. If the key is not found then the key is returned.

Type
:   string

This example returns "You entered <ok>" when the CONFIRM message text is "You entered %0"
and the inputValue variable value is "<ok>". Note this string must be used in a context where HTML escaping
is done to avoid XSS vulnerabilities.

#### (static) formatNoEscape(pPattern, …pValues) → {string}

Same as apex.lang.format, except the replacement arguments are not HTML escaped.
They must be known to be safe or are used in a context that is safe.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pPattern` | string |  | The message pattern. |
| `pValues` | \* | <repeatable> | Any number of replacement values, one for each message parameter %0 to %9. Non string arguments are converted to strings. |

##### Returns:

The formatted message text.

Type
:   string

This example returns "You entered <ok>" when the inputValue variable value is "<ok>".
Note this string must be used in a context where HTML escaping is done to avoid XSS vulnerabilities.

#### (static) getMessage(pKey) → {string}

Return the message associated with the given key.
The key is looked up in the messages added with the apex.lang.addMessages, apex.lang.loadMessages,
or apex.lang.loadMessagesIfNeeded functions.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pKey` | string | The message key. |

##### Returns:

The localized message text. If the key is not found then the key is returned.

Type
:   string

This example returns "OK" when the localized text for key OK_BTN_LABEL is "OK".

#### (static) hasMessage(pKey) → {boolean}

Return true if pKey exists in the messages added with the apex.lang.addMessages,
apex.lang.loadMessages, or apex.lang.loadMessagesIfNeeded functions.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pKey` | string | The message key. |

##### Returns:

true if the given message exists and false otherwise.

Type
:   boolean

This example checks for the existence of a message, "EXTRA_MESSAGE", before using it.

#### (static) loadMessages(pMessageKeys) → {Promise}

Load additional messages from the server.

When an APEX page loads it automatically loads any text messages that have attribute *Used in JavaScript*
set to on. This function is useful when there are strings that are not always needed on the client
but can be loaded on demand.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pMessageKeys` | Array.<string> | An array of message keys (names) to load. The message keys can end in "%" to load all the messages with keys that start with the given text. |

##### Returns:

promise resolved (with no data) when messages are available, rejected (with no data) if the
ajax request fails.

Type
:   Promise

This example loads two additional text messages with names "MY_MESSAGE1" and "MY_MESSAGE2".
Once they have been loaded it uses `getMessage` to get the message text.

This example loads all the messages for a component. The component has named all its
message keys with a common prefix "MY_COMPONENT_". So the following would load messages such as
"MY_COMPONENT_MESSAGE1", "MY_COMPONENT_MESSAGE2" and so on.

#### (static) loadMessagesIfNeeded(pMessageKeys, pCallback)

Load additional messages from the server only if they are not already loaded.

When an APEX page loads it automatically loads any text messages that have attribute *Used in JavaScript*
set to on. This function is useful when there are strings that are not always needed on the client
but can be loaded on demand.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pMessageKeys` | Array.<string> | An array of message keys (names) that are needed by pCallback. These messages will be loaded if needed. |
| `pCallback` |  | A no argument function that is called when all the keys have been loaded. If all the messages have already been loaded then this function is called right away. |

This example code could be put in a Dynamic Action Execute JavaScript Code action that runs
when a "More Details" button is pressed. It loads the "DETAILED_HELP_INFO" message and displays it in
an alert.

Documentation generated by JSDoc 4.0.3 on Wed Nov 27 2024 04:42:15 GMT+0000 (Coordinated Universal Time)

Oracle APEX Release 24.2, JavaScript API Reference

Copyright © 2003, 2025, Oracle and/or its affiliates. All rights reserved.