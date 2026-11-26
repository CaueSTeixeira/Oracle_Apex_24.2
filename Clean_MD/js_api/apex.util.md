<!-- Fonte: JavaScript API Reference 24.2, aexjs/apex.util.html -->

# Namespace: util

## QuickNav

### Functions

* applyTemplate
* arrayEqual
* cancelInvokeAfterPaint
* debounce
* escapeCSS
* escapeHTML
* escapeHTMLAttr
* getDateFromISO8601String
* getNestedObject
* getScrollbarSize
* htmlBuilder
* invokeAfterPaint
* showSpinner
* stripHTML
* throttle
* toArray

## apex.util

The apex.util namespace contains general utility functions of Oracle APEX.

### Namespaces

delayLinger

### Functions

#### (static) applyTemplate(pTemplate, pOptionsopt) → {string}

This function applies data to a template. It processes the template string given in
`pTemplate` by substituting
values according to the options in `pOptions`.
The template supports APEX server style placeholder and item substitution syntax.

This function is intended to process APEX style templates in the browser.
However, it doesn't have access to all the data that the server has. When substituting page items and column
items it uses the current value stored in the browser not what is in session state on the server.
It does not support the old non-exact substitutions (with no trailing dot e.g. &ITEM). It does not support
the old column reference syntax that uses #COLUMN_NAME#. It cannot call
`PREPARE_URL` (this must be done on the server).
Using a template to insert JavaScript into the DOM is not supported.
After processing the template all script tags are removed.

The format of a template string is any text intermixed with any number of replacement tokens
or directives. Two kinds of replacement tokens are supported: placeholders and data substitutions.
Directives control the processing of the template. Directives are processed first, then placeholders and finally
data substitutions.

### Placeholders

This is also known as a hash substitution.

Placeholder syntax is:

```
#<placeholder-name>#
```

The <placeholder-name> is an uppercase alpha numeric plus "_", and "$" string that must be a property
name in option object `placeholders` that gets replaced with the property value.
Any placeholder tokens that don't match anything in the placeholders object are left as is (searching for the
next placeholder begins with the trailing # character).

### Data substitutions

Substitution syntax is any of the following:

```
&<item-name>.
&<item-name>!<escape-filter>.
&"<quoted-item-name>".
&"<quoted-item-name>"!<escape-filter>.
&APP_TEXT$<message-key>.
&APP_TEXT$<message-key>!<escape-filter>.
&"APP_TEXT$<message-key>".
&"APP_TEXT$<message-key>"!<escape-filter>.
&{message-key <parameters>}.
&{"message-key" <parameters>}.
&{message-key <parameters>}!<escape-filter>.
&{"message-key" <parameters>}!<escape-filter>.
```

The <item-name> is an uppercase alpha numeric plus "_", "$", and "#" string. The <quoted-item-name>
is a string of any characters except carriage return, line feed, and double quote.
In both cases the item name is the name of a page item (unless option `includePageItems` is false),
a column item (if `model` and `record` options are given
or when looping over a model), a built-in substitution (unless option
`includeBuiltinSubstitutions` is false),
or an extra substitution (if option `extraSubstitutions` is given or within a
loop directive).

Note: While a quoted item name can contain almost any characters it cannot contain a placeholder or directive.
So for example `&"X#Y#Z".` will not work if there is a placeholder named
`Y` and `&"X{if Y/}Z".` will not work
because `if` is a directive.

The <item-name> can include a property reference. A "%" character separates the item-name from the property name.
For example `&P1_NAME%LABEL.` will return the label of the P1_NAME item.
The property name is case-insensitive for the following item and column properties. If the item value
is an object the property name is case-sensitive and accesses the value of the object property with that name.

The properties and the values they return for a page item are:

* **LABEL** - The item label.
* **DISPLAY** - The display value of the item's current value.
* **CHANGED** - "Y" if the item has been changed and "N" otherwise.
* **DISABLED** - "Y" if the item is disabled and "N" otherwise.

The properties for a column item are:

* **HEADING** - The column heading text. The heading may include markup. If there is no heading
  the label will be used if there is one.
* **LABEL** - The column label. If there is no label the heading will be used with markup removed.
* **DISPLAY** - The display value of the column value for the current row/record.
* **HEADING_CLASS** - Any CSS classes defined for the column heading.
* **COLUMN_CLASS** - Any CSS classes defined for the column.
* **REQUIRED** - "Y" if the column is required and "N" otherwise.

The <message-key> is a message key suitable for use in apex.lang.getMessage and
is replaced with the localized message text for the given key. The message must already be loaded on the
client by setting the Text Message attribute *Used in JavaScript* to On or otherwise adding it such as with
apex.lang.addMessages.
If no replacement for a substitution can be found it is replaced with the message key. The language specifier
that is supported for server side message substitutions is not supported by the client and will be ignored
if present.

The short Text Messages substitution syntax also support parameters. Before the closing brace, add name=value pairs, separated by white space. Names can contain any character except white space and "=".
Values can be one of the following:

* Unquoted substitution, HTML-escaped by default. For example:

  &P1_NAME.
* Quoted substitution, HTML-escaped by default. For example:

  &"X-1".
* Unquoted literal value. Anything except double quotes. White space and closing curly brace is supported. For example:

  he&she+it?
* Quoted literal value. The value is enclosed in double quotes. To insert a double quote, type it twice. For example:

  "Hello ""APEX"" world"

The following is an example for a complex text message with parameters:

```
&{TEXT->MSG
Unquoted_Substitution=&P1_NAME!RAW.
Quoted_Substitution=&"Quoted name"!RAW.
Unquoted_Literal=how/do.you!do?
Quoted_Literal="Jerry Garcia
Ron ""Pigpen"" McKerhan"}!HTML.
```

When substituting a column item the given record of the given model is used to find a matching column name.
If not found and if the model has a parent model then the parent model's columns are checked.
This continues as long as there is a parent model. The order to resolve a data substitution is: message key,
column item, column item from ancestor models, page item, built-in substitutions, and finally extra substitutions.
For backward compatibility column items support the "_LABEL" suffix to access the defined column label.
For example if there is a column item named `NOTE` the substitution
`&NOTE_LABEL.` will return the label string for column `NOTE`.
It is better to use the label property in this case, for example: `&NOTE%label.`.

The built-in substitution names are:

* &APP_USER.
* &APP_ID.
* &APP_PAGE_ID.
* &APP_SESSION.
* &APP_FILES.
* &WORKSPACE_FILES.
* &REQUEST.
* &DEBUG.
* &APEX_FILES.
* &IMAGE_PREFIX. (legacy- use &APEX_FILES. instead)
* &APEX_VERSION.
* &APEX_BASE_VERSION.

See apex.env for the meaning of these substitutions.

The escape-filter controls how the replacement value is escaped or filtered. It can be one of the following
values:

* HTML the value will have HTML characters escaped using apex.util.escapeHTML.
* ATTR the value will be escaped for an HTML attribute value context using apex.util.escapeHTMLAttr.
* RAW does not change the value at all.
* STRIPHTML the value will have HTML tags removed and HTML characters escaped.

This will override any default escape filter set with option `defaultEscapeFilter`
or from the column definition `escape` property.

### Directives

Directive syntax is:

```
{<directive-name>[ <directive-arguments>]/}
```

The directive name determines what it does as described below. Directive names are case-insensitive.
There can be no whitespace between the open bracket "{" and the directive name.
Directives often come in sets that work together. A directive may have additional arguments.

#### If condition directives

Syntax:

```
{if [!][?|=]NAME/}
TRUE_TEMPLATE_TEXT
{elseif [!][?|=]NAME2/}
ELSE_TRUE_TEMPLATE_TEXT
{else/}
FALSE_TEMPLATE_TEXT
{endif/}
```

The entire text from the **if** directive to the matching **endif** directive is
replaced with the processed template text following the first **if** or **elseif**
directive that evaluates to true or the template text following the **else**
directive if none are true. There must be an **if** and **endif** directive.
The **elseif** and **else** directives are optional.
There can be any number of **elseif** directives. The directives must go in the order shown.
**If** directives can be nested.
That means any of the template texts can contain another **if** directive.

The **if** and **elseif** directives test the value of NAME
and if it is true process the following template text.
The NAME can be an item-name, quoted-item-name, or placeholder-name. The value of an item-name or quoted-item-name
is the value of that page item or column item. The value of a placeholder-name is the text of the placeholder.
If no data substitution or placeholder with that name exists then the value is empty string.

A value is false if after trimming leading and trailing spaces it is an empty string,
or for a page item the item item#isEmpty method returns true,
or if the value is equal to any of the values in the `falseValues` option.
Any value that is not false is true. If the name is prefixed with exclamation mark (!) operator then the logic is
negated and the following template text is processed if the value is false.

The if condition directive handles both empty (or not empty) tests and Boolean true/false tests (using the
convention of character true/false values such as 'Y'/'N') at the same time. This results in confusion for
rare case where the intention is to test for not empty but the actual value is 'N', which is not empty but
still considered false. The optional '?' prefix operator can be used to explicitly test if the value is empty.
The optional '=' prefix operator can be used to explicitly test if the value is true or false.

Example:
The page contains items P1_TITLE, P_ICON, P1_DESCRIPTION, and P1_DETAILS and all have optional values.
The template outputs a default title if P1_TITLE is empty. An optional icon is shown only if there is a title.
The template output includes markup for the description if it is not empty or details if it is not empty and
nothing otherwise.

```
<h3>{if ?P1_TITLE/}&P1_TITLE. {if P1_ICON/}<span class="fa &P1_ICON."></span>{endif/}
{else/}Untitled{endif/}</h3>
{if P1_DESCRIPTION/}
  <p class="description">&P1_DESCRIPTION.</p>
{elseif P1_DETAILS/}
  <p class="details">&P1_DETAILS.</p>
{endif/}
```

#### Case condition directives

Syntax:

```
{case NAME/}
{when string1/}
TEMPLATE_TEXT1
{when string2/}
TEMPLATE_TEXT2
{otherwise/}
TEMPLATE_TEXT
{endcase/}
```

The entire text from the **case** directive to the matching **endcase** directive
is replaced with the processed template text after the **when** directive that matches the NAME value.
The value of NAME is compared with each of the strings in the **when** directive and if it is equal the following
template (TEMPLATE_TEXTn) is processed. If no **when** directive matches then the template after
the **otherwise** directive is processed if there is one. The **otherwise** directive is optional
but it must come at the end and there can only be one. **Case** directives can be nested.
That means any of the template texts can contain another **case** directive.

The NAME can be an item-name, quoted-item-name, or placeholder-name. The value of an item-name or quoted-item-name
is the value of that page item or column item. The value of a placeholder-name is the text of the placeholder.
If no data substitution or placeholder with that name exists then the value is empty string. The NAME value and each string
is trimmed of leading and trailing spaces before comparison. The comparison is case-sensitive.

Example:
The page contains items P1_NAME and P1_DETAILS, and P1_DETAIL_STYLE that can have a value of "FULL" or "BRIEF".
The intention is to control the markup according to the detail style.

```
{case P1_DETAIL_STYLE/}
{when FULL/}
    <div class="full">
        <span>&P1_NAME!HTML.</span>
        <p class="description">&P1_DETAILS!HTML.</p>
    </div>
{when BRIEF/}
  <div class="brief">
      <span>&P1_NAME!HTML.</span>
  </div>
{endcase/}
```

#### Loop directives

Syntax:

```
{loop ["SEP"] NAME/}
TEMPLATE_TEXT
{endloop/}
```

or

```
{loop MODEL_ID/}
TEMPLATE_TEXT
{endloop/}
```

The entire text from the **loop** directive to the matching **endloop** directive is
replaced with the template text evaluated once for each item in the NAME value or each record in the
model with id MODEL_ID.

In the first syntax, the NAME can be an item-name, quoted-item-name, or placeholder-name.
The value of an item-name or quoted-item-name is the value of that page item or column item.
The value of a placeholder-name is the text of the placeholder.
If no data substitution or placeholder with that name exists then the value is empty string. The NAME value should
be a separator delimited string that contains a list of items. The optional SEP argument defines the separator
character. If no SEP is given and NAME is an item, then the item's item#getMultiValueStorage method is used
to determine the separator, otherwise the default separator ":" is used. If SEP is more than one character it is
treated as a regular expression.

Within the loop there are two extra data substitutions available:

* **APEX$ITEM** - This is the value of the current item in the list.
* **APEX$I** - This is 1 based index of the current item in the list.

In the second syntax, the MODEL_ID identifies a model created with apex.model.create (this
includes models created by regions such as Interactive Grid and Cards).
If the MODEL_ID is omitted then the model passed in the `pOptions.model`
property is used. A model name can either be a string or, for detail models, an array of this
form: `["name", "instance"]` (see model.ModelId).
The MODEL_ID allows data substitutions as shown in the nested loop example below.

Within the loop there are three extra data substitutions available:

* **APEX$ID** - This is the identity of the record. See model#getRecordId.
* **APEX$I** - This is 1 based index of the current record.
* **APEX$META** - This is an object with metadata about the current record. The metadata
  comes from model.RecordMetadata but in a form that is easier to use from templates.
  The object has these properties (case is significant):
  + **valid** - This is "Y" (true) unless the record is deleted, an aggregate record
    or has an error or warning.
  + **state** - This is "O" for original, "D" for deleted, "I" for inserted,
    "U" for updated and empty string for non-data records.
  + **allowedOperations** - This is one of "" for no editing, "U" update only,
    "D" for delete only, "UD" for update and delete.
  + **selected** - This is "Y" (true) if the record is selected and "N" otherwise.
    This only applies if the view widget is keeping the selected state in the model.
  + **agg** - This is the aggregate name of an aggregate record (example: "SUM")
    or empty string otherwise.
  + **highlight** - This is the highlight name.
  + **endControlBreak** - This is "Y" (true) if this record marks the end of a control break.
  + **grandTotal** - This is "Y" (true) if this is an aggregate record and it is
    the grand total (overall value) for the aggregate.
  + **errorMessage** - This is the error message for the record if there is one.
  + **warningMessage** - This is the warning message for the record if there is one.

Example:
The following example takes a page item, `P1_TAGS` that contains a bar "|"
separated list of tags such as "apples|cherries|pears" and turns it into an HTML list that can be nicely styled.

```
<ul class="tags">{loop "|" P1_TAGS/}
  <li class="tag-item">&APEX$ITEM.</li>
{endloop/}</ul>
```

Example:
The following example loops over a model with id "emp_grid" and turns it into a list of names.
The model includes EMPNO and ENAME columns. Aggregate and deleted records are not included.

```
<ul>{loop emp_grid/}{if APEX$META%valid/}
<li id="list_&EMPNO!ATTR.">&ENAME.</li>
{endif/}{endloop/}</ul>
```

Example:
The following example shows a nested loop over master and detail models. This uses the sample DEPT and EMP
tables. It produces nested UL list elements.

Note the inner loop uses &DEPTNO. from the outer loop to form the model id of the detail model.

Note loops over models only include records that have already been fetched from the server and
detail models that have been created.

For brevity the {if APEX$META%valid/} is omitted from the inner loop.

```
<ul>{loop dept_grid/}{if APEX$META%valid/}
<li>&DNAME. - &LOC.:<ul>{loop ["emp_grid", "&DEPTNO."]/}
  <li>&ENAME.</li>
  {endloop/}</ul></li>
{endif/}{endloop/}</ul>
```

#### Comments

Syntax:

```
{!<comment-text>/}
```

This directive is substituted with nothing. It allows adding comments to templates.
The comment-text can be any characters except new line and the "/}" sequence.

Example:
This example includes a comment reminding the developer to complete something. In this case
replace a hard coded English string with a localizable text message.

```
<span>Name: &P1_NAME.</span> {!to do replace Name: with text message/}
```

#### Escape open bracket "{"

Syntax:

```
{{/}
```

In rare cases a lone open bracket "{" can be confused for the start of a directive if another directive
follows it on the same line.

Example:
This is an example where the open bracket "{" has to be escaped.

```
<span>The coordinates {{/}c, d} = {if VAL/}&VAL.{else/}unknown{endif/}</span>
```

Here are similar cases that don't require an escape.

```
<span>The coordinates { c, d } = {if VAL/}&VAL.{else/}unknown{endif/}</span>
```

```
<span>The coordinates {c, d} =
{if VAL/}&VAL.{else/}unknown{endif/}</span>
```

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pTemplate` | string |  | A template string with any number of replacement tokens as described above. |
| `pOptions` | Object | <optional> | An options object with the following properties that specifies how the template is to be processed:Properties  | Name | Type | Attributes | Description | | --- | --- | --- | --- | | `placeholders` | Object | <optional> | An object map of placeholder names to values. The default is null. | | `directives` | boolean | <optional> | Specify if directives are processed. If true directives are processed. If false directives are ignored and remain part of the text. The default is true. | | `defaultEscapeFilter` | string | false | <optional> | One of the above escape-filter values or false. The default is HTML. This is the escaping/filtering that is done if the substitution token doesn't specify an escape-filter. If a model column definition has an `escape` property then it will override the default escaping. This can also be false to turn off escaping (even when the substitution token includes an escape-filter) for the case where the return value of `applyTemplate` is going to be escaped. Setting `defaultEscapeFilter` to false avoids double escaping when the template result is going to be passed to an API that does its own escaping. Note: when false the STRIPHTML escape-filter will still strip HTML tags, but it will not HTML escape the result. | | `includePageItems` | boolean | <optional> | If true the current value of page items are substituted. The default is true. | | `model` | model | <optional> | The model interface used to get column item values. The default is null. | | `record` | model.Record | <optional> | The record in the model to get column item values from. Option `model` must also be provided. The default is null. | | `extraSubstitutions` | Object | <optional> | An object map of extra substitutions. The default is an empty object. | | `includeBuiltinSubstitutions` | boolean | <optional> | If true built-in substitutions such as APP_ID are done. The default is true. | | `falseValues` | Array.<string> | <optional> | An array of values that are considered false in if directive tests. Empty string and an item that doesn't exist are always considered false. The default is ["F", "f", "N", "n", "0"] | | `iterationCallback` | function | <optional> | A function called during loop directive iteration before each item or record and just once before processing a template when options `model` and `record` are provided. The function signature is:   `callback(loopArg, model, record, index, placeholders, extraSubstitutions)`. The `index` parameter is the 0 based index of the item or record in the collection being iterated over. The `extraSubstitutions` parameter is an object that contains the properties in the extraSubstitutions option passed to applyTemplate as well as any extra data substitutions defined by the loop directive. This allows making additional substitutions available to the template by assigning a value to a property of `extraSubstitutions`. When looping over an item value the model and record parameters will be null. When called once before template processing (when options `model` and `record` are provided) the loopArg and index parameters will be null. | |

##### Returns:

The template string with replacement tokens substituted with data values.

Type
:   string

This example inserts an image tag where the path to the image comes from the built-in
APEX_FILES substitution and a page item called P1_PROFILE_IMAGE_FILE.

This example inserts a div with a message where the message text comes from a
placeholder called MESSAGE.

#### (static) arrayEqual(pArray1, pArray2) → {boolean}

Compare two arrays and return true if they have the same number of elements and
each element of the arrays is strictly equal to each other. Returns false otherwise.
This is a shallow comparison.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pArray1` | Array | The first array. |
| `pArray2` | Array | The second array. |

##### Returns:

true if a shallow comparison of the array items are equal

Type
:   boolean

This example returns true.

This example returns false.

#### (static) cancelInvokeAfterPaint(pId)

Wrapper around cancelAnimationFrame that can fallback to `clearTimeout`.
Cancels the callback using the id returned from apex.util.invokeAfterPaint.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pId` | \* | The id returned from apex.util.invokeAfterPaint. |

See example for function apex.util.invokeAfterPaint

#### (static) debounce(pFunction, pDelay, pImmediateopt) → {function}

Returns a new function that calls `pFunction` but not until
`pDelay` milliseconds after the last time the returned function is
called when `pImmediate` is false.
If `pImmediate` is true then `pFunction`
will be called first and will not be called again until `pDelay` milliseconds
after the last time the returned function is called.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pFunction` | function |  | The function to call. |
| `pDelay` | number |  | The time to wait before or after calling the function in milliseconds. |
| `pImmediate` | boolean | <optional> | The boolean that determines whether to call the function before or after the delay. Defaults to false. |

##### Returns:

The debounced version of `pFunction`.

Type
:   function

This example calls the function formatValue in response to the user typing characters but only
after the user pauses typing. In a case like this formatValue would also be called from the blur event on the same item.

#### (static) escapeCSS(pValue) → {string}

Returns string `pValue` with any CSS meta-characters escaped.
Use this function when the value is used in a CSS selector.
Whenever possible if a value is going to be used as a selector, constrain the value so
that it cannot contain CSS meta-characters making it unnecessary to use this function.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pValue` | string | The string that may contain CSS meta-characters to be escaped. |

##### Returns:

The escaped string, or an empty string if pValue is null or undefined.

Type
:   string

This example escapes an element id that contains a (.) period character so that it finds the
element with id = "my.id". Without using this function the selector would have a completely
different meaning.

#### (static) escapeHTML(pValue) → {string}

Returns string `pValue` with any special HTML characters in element content
context escaped to prevent cross site scripting (XSS) attacks. It escapes the characters: ampersand,
double quote, quote, less than, greater than, and forward slash.
It provides the same functionality as `APEX_ESCAPE.HTML` (in extended mode) in PL/SQL.

This function should always be used when inserting untrusted data into the DOM in element content context.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pValue` | string | The string that may contain special HTML characters to be escaped. Null is converted to empty string. |

##### Returns:

The escaped string.

Type
:   string

This example appends text to a DOM element where the text comes from a page item called
P1_UNTRUSTED_NAME. Data entered by the user cannot be trusted to not contain malicious markup.

#### (static) escapeHTMLAttr(pValue) → {string}

Returns string `pValue` with any special HTML characters in attribute value
context escaped to prevent cross site scripting (XSS) attacks. It hex escapes everything that is not
alphanumeric or one of the following characters: comma, period, dash, underscore.
It provides the same functionality as `APEX_ESCAPE.HTML_ATTRIBUTE` in PL/SQL.

This function should always be used when inserting untrusted data into the DOM in attribute value context.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pValue` | string | The string that may contain special HTML characters to be escaped. |

##### Returns:

The escaped string.

Type
:   string

This example sets the title of a DOM element where the text comes from a page item called
P1_UNTRUSTED_NAME. Data entered by the user cannot be trusted to not contain malicious markup.

#### (static) getDateFromISO8601String(pDateStr) → {Date}

Get a JavaScript Date object corresponding to the input date string which must be in simplified ISO 8601 format.
In the future Date.parse could be used but currently there are browsers we support that don't yet support the ISO 8601 format.
This implementation is a little stricter about what parts of the date and time can be defaulted. The year, month, and day are
always required. The whole time including the T can be omitted but if there is a time it must contain at least the hours
and minutes. The only supported time zone is "Z".
This function is useful for turning the date strings returned by the
`APEX_JSON.STRINGIFY` and `APEX_JSON.WRITE`
procedures that take a DATE value into Date objects that the client can use.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pDateStr` | string | String representation of a date in simplified ISO 8601 format |

##### Returns:

Date object corresponding to the input date string.

Type
:   Date

This example returns a date object from the date string in result.dateString. For example
"1987-01-23T13:05:09.040Z"

#### (static) getNestedObject(pRootObject, pPath) → {Object}

Returns the nested object at the given path `pPath` within the nested object structure in
`pRootObject` creating any missing objects along the path as needed.
This function is useful when you want to set the value of a property in a deeply
nested object structure and one or more of the nested objects may or may not exist.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pRootObject` | Object | The root object of a nested object structure. |
| `pPath` | string | A dot (".") separated list of properties leading from the root object to the desired object to return. |

##### Returns:

Type
:   Object

This example sets the value of `options.views.grid.features.cellRangeActions`
to `false`.
It works even when the options object does not contain a views.grid.features object or a views.grid object
or even a views object.

#### (static) getScrollbarSize() → {object}

Gets the system scrollbar size for cases in which the addition or subtraction of a scrollbar
height or width would affect the layout of elements on the page. The page need not have a scrollbar on it
at the time of this call.

##### Returns:

An object with height and width properties that describe any scrollbar on the page.

Type
:   object

The following example returns an object such as `{ width: 17, height: 17 }`. Note
the actual height and width depends on the Operating System and its various display settings.

#### (static) htmlBuilder() → {htmlBuilder}

Return an htmlBuilder interface.

##### Returns:

Type
:   htmlBuilder

#### (static) invokeAfterPaint(pFunction) → {\*}

Wrapper around requestAnimationFrame that can fallback to `setTimeout`.
Calls the given function before next browser paint. See also apex.util.cancelInvokeAfterPaint.

See HTML documentation for `window.requestAnimationFrame` for details.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pFunction` | function | function to call after paint |

##### Returns:

id An id that can be passed to apex.util.cancelInvokeAfterPaint

Type
:   \*

This example will call the function myAnimationFunction before the next browser repaint.

#### (static) showSpinner(pContaineropt, pOptionsopt) → {jQuery}

Function that renders a spinning alert to show the user that processing is taking place. Note that the alert is
defined as an ARIA alert so that assistive technologies such as screen readers are alerted to the processing status.

The spinner can be used with apex.util.delayLinger for better control over if, when, and for how long
it is shown.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pContainer` | string | jQuery | Element | <optional> | Optional jQuery selector, jQuery, or DOM element identifying the container within which you want to center the spinner. If not passed, the spinner will be centered on the whole page. The default is $("body"). |
| `pOptions` | Object | <optional> | Optional object with the following properties:Properties  | Name | Type | Attributes | Description | | --- | --- | --- | --- | | `alert` | string | <optional> | Alert text visually hidden, but available to Assistive Technologies. Defaults to "Processing". | | `spinnerClass` | string | <optional> | Adds a custom class to the outer SPAN for custom styling. | | `fixed` | boolean | <optional> | If true the spinner will be fixed and will not scroll. When fixed is true the pContainer parameter is ignored and the spinner is always appended to the body. | |

##### Returns:

A jQuery object for the spinner. Use the jQuery remove method when processing is complete.

Type
:   jQuery

To show the spinner when processing starts.

To remove the spinner when processing ends.

#### (static) stripHTML(pText) → {string}

Returns string `pText` with all HTML tags removed.

##### Parameters:

| Name | Type | Description |
| --- | --- | --- |
| `pText` | string | The string that may contain HTML markup that you want removed. |

##### Returns:

The input string with all HTML tags removed.

Type
:   string

This example removes HTML tags from a text string.

#### (static) throttle(pFunction, pWait, pImmediateopt) → {function}

Returns a new function that calls `pFunction` then waits
`pWait` milliseconds from the initial function call before
executing again when `pImmediate` is true.

If `pImmediate` is false then the call to `pFunction`
will not happen until `pWait` milliseconds after the initial
function call.
Functions are executed at timed intervals, so if the throttle action is fired during
`pWait`, the most recent call is stored and called after
`pWait` is done. This is different from apex.util.debounce,
which only calls a function once at the end of a single or series of events.

##### Parameters:

| Name | Type | Attributes | Description |
| --- | --- | --- | --- |
| `pFunction` | function |  | The function to call. |
| `pWait` | number |  | The time to wait before or after calling the function in milliseconds. |
| `pImmediate` | boolean | <optional> | The boolean that determines whether to call the function before or after the delay. Defaults to true. |

##### Returns:

The throttled version of `pFunction`.

Type
:   function

This example calls the function updatePosition in response to the user scrolling but only
calls the function once every 2 seconds if the scroll event is fired multiple times.

#### (static) toArray(pValue, pSeparatoropt) → {Array}

Function that returns an array based on the value passed in `pValue`.

##### Parameters:

| Name | Type | Attributes | Default | Description |
| --- | --- | --- | --- | --- |
| `pValue` | string | \* |  |  | If this is a string, then the string will be split into an array using the `pSeparator` parameter. If it's not a string, then we try to convert the value with `apex.jQuery.makeArray` to an array. If pValue is null, undefined or an empty string, then we return an empty array. When pValue is an array then we return it. |
| `pSeparator` | string | object | RegExp | <optional> | ":" | Separator used to split a string passed in `pValue`, defaults to colon if not specified. Only needed when `pValue` is a string. When passing an object then this must include the following properties:  * type {string}: The type or format of the `pValue` string.   One of "separated" or "json-array" * separator {string} (optional): when `type` is "separated"   then this separator is used to split the passed in string. It is ignored otherwise.  You can also use item#getMultiValueStorage, because it returns this object. This can also be a regular expression suitable for the `String split` function. |

##### Returns:

Type
:   Array

This example splits the string into an array with 3 items:
`["Bags","Shoes","Shirts"]`.

This example splits the string into an array just like in the previous example. The only
difference is the separator character is ",".

This example splits the string into an array just like in the previous example. The only
difference is that storage type "json-array" is used.

This example splits the string into an array just like in the previous example. The only
difference is that the separator character is "~" and pSeparator is an object.

This example returns the jQuery object as an array.

This example splits a string value into an array. The difference is
the item#getMultiValueStorage function is used to get the separator from an item.

This example splits a comma separated string value into an array allowing extra space
characters after each comma.

Documentation generated by JSDoc 4.0.3 on Wed Nov 27 2024 04:42:15 GMT+0000 (Coordinated Universal Time)

Oracle APEX Release 24.2, JavaScript API Reference

Copyright © 2003, 2025, Oracle and/or its affiliates. All rights reserved.