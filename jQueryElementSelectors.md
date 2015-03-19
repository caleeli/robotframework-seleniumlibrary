

# Introduction #

Selenium Library 2.3 introduces an ability to register and use a custom location strategy to locate elements on the website. The new strategy must be loaded by selenium-server.jar. This guide will explain how to enable location strategy based on jQuery.

# Create user-extensions.js #

Download jQuery (uncompressed) and rename it to user-extensions.js. Then open the file and append the following selector function:

```
Selenium.prototype.locateElementByJQuerySelector = function(locator, inDocument, inWindow) {
    var loc = locator.replace(/&gt;/g, '>');
    loc = loc.replace(/&lt;/g, '<');
    var element;
    try {
        element = $(inDocument).find(loc);
    } catch (e) {
        return null;
    }
    if (element.length == 1 ) {
        return element[0];
    } else if(element.length > 1) {
        return element.get();
    } else {
        return null;
    }
}
```

# Using Add Location Strategy keyword #

Selenium server must be told to load user-extensions.js file at startup. That is done by adding arguments to Start Selenium Server keyword.

| Start Selenium Server | -userExtensions | ${CURDIR}${/}user-extensions.js |
|:----------------------|:----------------|:--------------------------------|

New location strategy must be registered with `Add Location Strategy` keyword. It's important to do that AFTER the browser window is opened.

| Add Location Strategy | jquery | return Selenium.prototype.locateElementByJQuerySelector(locator, inDocument, inWindow); |
|:----------------------|:-------|:----------------------------------------------------------------------------------------|

To use the new location prefix the jQuery locator with "jquery=" string:
| Page Should Contain Element | jquery=div.#data-table > table |
|:----------------------------|:-------------------------------|