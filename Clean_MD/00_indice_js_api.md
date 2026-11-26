# Índice JavaScript API (24.2) — namespaces e membros
Fonte: https://docs.oracle.com/en/database/oracle/apex/24.2/aexjs/
Use apenas o que consta aqui. JavaScript é último recurso.

## apex.item
- (static) addAttachHandler(pHandler)
- (static) create(pItemId, pItemImpl) → {object}
- (static) isItem(pItemId) → {boolean}

## item
- element :jQuery
- id :string|false
- item_type :string
- node :Element|false
- value :string|Array
- addValue(pValue, pDisplayValueopt)
- disable()
- displayValueFor(pValue, pState) → {string}
- enable()
- getMultiValueStorage() → {object|null}
- getSeparator() → {string|null}
- getValidationMessage(pLabelopt) → {string}
- getValidity() → {object}
- getValue() → {string|Array}
- hasDisplayValue() → {boolean}
- hide(pHideRowopt)
- isChanged() → {boolean}
- isDisabled() → {boolean}
- isEmpty() → {boolean}
- isReady() → {boolean}
- refresh()
- removeValue(pValueopt)
- setFocus()
- setStyle(pPropertyName, pPropertyValue)
- setValue(pValue, pDisplayValueopt, pSuppressChangeEventopt)
- show(pShowRowopt)
- whenReady() → {Promise}

## apex.page
- (static) cancelWarnOnUnsavedChanges()
- (static) confirm(pMessageopt, pOptionsopt)
- (static) isChanged() → {boolean}
- (static) submit(pOptionsopt) → {boolean|undefined}
- (static) validate(pLocationopt) → {boolean}
- (static) warnOnUnsavedChanges(pMessageopt, pExtraIsChangedopt)

## apex.server
- (static) chunk(Text) → {string|Array.<string>}
- (static) loadScript(pOptions, callbackopt) → {*}
- (static) plugin(pAjaxIdentifieropt, pDataopt, pOptionsopt) → {Promise}
- (static) pluginUrl(pAjaxIdentifier, pDataopt) → {string}
- (static) process(pName, pDataopt, pOptionsopt) → {Promise}
- (static) url(pDataopt, pPageopt) → {string}

## apex.message
- (static) TYPE :object
- (static) addVisibilityCheck(pFunction)
- (static) alert(pMessage, pCallback, pOptionsopt)
- (static) ariaAlertMessage(pMessage)
- (static) ariaMessage(pMessage)
- (static) clearErrors()
- (static) confirm(pMessage, pCallback, pOptionsopt)
- (static) hidePageSuccess()
- (static) setDismissPreferences(pOptions)
- (static) setThemeHooks(pOptions)
- (static) showErrors(pErrors)
- (static) showPageSuccess(pMessage)

## apex.da
- (static) cancel()
- (static) handleAjaxErrors(pjqXHR, pTextStatus, pErrorThrown, pResumeCallback)
- (static) resume(pCallback, pErrorOccurred)

## apex.region
- (static) create(pRegionId, pRegionImpl)
- (static) destroy(pRegionId)
- (static) findClosest(pTarget) → {region|null}
- (static) isRegion(pRegionId) → {boolean}

## region
- element :jQuery
- filterRegionId :string
- parentRegionId :string
- type :string
- widgetName :string
- alternateLoadingIndicator(pElement, pLoadingIndicator$) → {jQuery}
- call(pMethod, …args) → {*}
- focus()
- off(events, …args)
- on(events, …args)
- refresh(pKeepPagination) → {Promise}
- widget() → {jQuery|null}

## apex.util
- (static) applyTemplate(pTemplate, pOptionsopt) → {string}
- (static) arrayEqual(pArray1, pArray2) → {boolean}
- (static) cancelInvokeAfterPaint(pId)
- (static) debounce(pFunction, pDelay, pImmediateopt) → {function}
- (static) escapeCSS(pValue) → {string}
- (static) escapeHTML(pValue) → {string}
- (static) escapeHTMLAttr(pValue) → {string}
- (static) getDateFromISO8601String(pDateStr) → {Date}
- (static) getNestedObject(pRootObject, pPath) → {Object}
- (static) getScrollbarSize() → {object}
- (static) htmlBuilder() → {htmlBuilder}
- (static) invokeAfterPaint(pFunction) → {*}
- (static) showSpinner(pContaineropt, pOptionsopt) → {jQuery}
- (static) stripHTML(pText) → {string}
- (static) throttle(pFunction, pWait, pImmediateopt) → {function}
- (static) toArray(pValue, pSeparatoropt) → {Array}

## apex.event
- (static) trigger(pSelector, pEvent, pDataopt) → {boolean}

## apex.debug
- (static) LOG_LEVEL :object
- (static) error(…arguments)
- (static) getLevel() → {number}
- (static) info(…arguments)
- (static) log(…arguments)
- (static) message(pLevel, …arguments)
- (static) setLevel(pLevel)
- (static) trace(…arguments)
- (static) warn(…arguments)

## apex.navigation
- (static) dialog(pUrl, pOptions, pCssClasses, pTriggeringElement)
- (static) popup(pOptions) → {Object|null}
- (static) openInNewWindow(pURL, pWindowNameopt, pOptionsopt) → {Object|null}
- (static) redirect(pWhere, pIgnoreUnsavedChanges)

## apex.lang
- (static) addMessages(pMessages)
- (static) clearMessages()
- (static) format(pPattern, …pValues) → {string}
- (static) formatMessage(pKey, …pValues) → {string}
- (static) formatMessageNoEscape(pKey, …pValues) → {string}
- (static) formatNoEscape(pPattern, …pValues) → {string}
- (static) getMessage(pKey) → {string}
- (static) hasMessage(pKey) → {boolean}
- (static) loadMessages(pMessageKeys) → {Promise}
- (static) loadMessagesIfNeeded(pMessageKeys, pCallback)