


# SeleniumLibrary 2.3.1 #

SeleniumLibrary 2.3.1 was released 2010-03-10.

The most important thing in the release is the upgrade of the embedded
Selenium Server to version 1.0.3, to fix [issue 60](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=60) and [issue 99](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=99). The 1.0.3
version of Selenium Server is three times the size of 1.0.1, which means that
SeleniumLibrary distribution also triples it's size, from ~5MB to ~15MB.

In addition to server upgrade some minor enhancements and bug fixes are
included.

## Acknowledgments ##

Thanks to everyone who submitted or commented on issues. Special thanks to
Andreas Ebbert-Karroum for sending patch to fix [issue 98](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=98) and to user jerry57
for testing [issue 60](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=60).

## List of all fixes and enhancements ##

| **ID** | **Type** | **Priority** | **Summary** |
|:-------|:---------|:-------------|:------------|
| [Issue 98](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=98) | Defect | High | Parsing Selenium errors containing Unicode fails |
| [Issue 99](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=99) | Enhancement | High | Support Firefox 3.6 by updating the embedded Selenium Server to 1.0.3 version |
| [Issue 60](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=60) | Defect | Medium | Open Browser fails to open Firefox 3.5.4 on OS X 10.6.1 |
| [Issue 84](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=84) | Defect | Medium | Browser handling keywords do not honor timeout set in library import |
| [Issue 100](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=100) | Enhancement | Medium | Possibility to set log level to potentially big messages by `Page Should Contain` |
| [Issue 101](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=101) | Documentation | Medium | Document that `Capture Screenshot` doesn't create intermediate directories since 2.3 |

Altogether 6 issues.

# SeleniumLibrary 2.3 #

SeleniumLibrary 2.3 was released 2010-02-15.

The original plan was to have just a 2.2.3 minor release, but the high interest for new keywords and other enhancements/fixes turned this into a new major release.

## Acknowledgments ##

[Radek Wierzbicki](http://radekw.com) provided a patch to support custom element location strategies ([issue 59](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=59)), and wrote a [wiki page](jQueryElementSelectors.md) about how to use this new `Add Location Strategy` keyword to enable jQuery selectors. He has also written about this subject in [his blog](http://radekw.com/blog/2009/11/03/jquery-selectors-in-selenium).

[Andreas Ebbert-Karroum](http://blogs.karroum.de/andreas) created the original patch to support remote screenshots ([issue 89](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=89)), and helped testing also the new `Capture Page Screenshot` keyword ([issue 93](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=93)). He is probably just happy that his earlier blog post about [remote screenshots with SeleniumLibrary 2.2](http://blog.codecentric.de/en/2010/02/remote-screenshots-mit-selenium-und-dem-robot-framework/) is nowadays slightly outdated and taking remote screenshots works out-of-the-box.

Kai Hackemesser debugged a nasty socket leak problem on Jython ([issue 79](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=79)) that turned out to be a bug in the Selenium RC Python API ([issue 817](http://jira.openqa.org/browse/SRC-817) in the Selenium RC issue tracker). Kai also wrote the original patch fixing the issue.

Big thanks also to everyone else who submitted code, bug reports, feature requests, or otherwise helped making this great release.

## Backwards incompatible changes ##

Support for attribute syntax inherited from PamieLibrary (the previous web testing library for Robot Framework what was never open source) was removed ([issue 58](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=58)). It had already been deprecated in the 2.2 release.

## List of all fixes and enhancements ##

| **ID** | **Type** | **Priority** | **Summary** |
|:-------|:---------|:-------------|:------------|
| [Issue 72](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=72) | Defect | High | `Wait Until Page Contains` doesn't always work |
| [Issue 79](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=79) | Defect | High | Selenium Python API leaks sockets on Jython because connections to SeleniumServer are not closed explicitly |
| [Issue 73](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=73) | Enhancement | High | `Open Context Menu` keyword |
| [Issue 74](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=74) | Enhancement | High | Possibility to call Selenium API directly (`Call Selenium API` keyword) |
| [Issue 80](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=80) | Enhancement | High | `Get Element Attribute` keyword |
| [Issue 70](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=70) | Defect | Medium | `Page Should (Not) Contain Button` keywords don't work with buttons created like `<input type="button">` |
| [Issue 94](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=94) | Defect | Medium | IE doesn't support accessing images and links with relative `src` and `href` attributes |
| [Issue 58](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=58) | Enhancement | Medium | Deprecate PAMIE attribute syntax |
| [Issue 59](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=59) | Enhancement | Medium | `Add Location Strategy` keyword |
| [Issue 63](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=63) | Enhancement | Medium | `Wait until page contains element` keyword |
| [Issue 68](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=68) | Enhancement | Medium | `_SELENIUM_LOCATOR_PREFIXES` needs to be extensible |
| [Issue 69](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=69) | Enhancement | Medium | `Get matching xpath count` keyword |
| [Issue 71](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=71) | Enhancement | Medium | `Start Selenium Server` should use the port given to the library when it is taken into use |
| [Issue 77](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=77) | Enhancement | Medium | `Get Horizontal Position` and `Get Vertical Position` keywords |
| [Issue 78](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=78) | Enhancement | Medium | `Start Selenium Server` keyword should log the path to the Seleniun server log (and it's doc should have usage examples) |
| [Issue 83](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=83) | Enhancement | Medium | Possibility to give custom error message to `Wait For Condition` and `Wait Until Page Contains` keywords |
| [Issue 85](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=85) | Enhancement | Medium | `Go Back` keyword |
| [Issue 89](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=89) | Enhancement | Medium | Support for taking screenshots on remote systems to `Capture Screenshot` keyword |
| [Issue 92](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=92) | Enhancement | Medium | Possibility to use non-default selenium-server.jar with `Start Selenium Server` |
| [Issue 93](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=93) | Enhancement | Medium | `Capture Page Screenshot` keyword |
| [Issue 65](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=65) | Documentation | Medium | Bad example about using XPath in library documentation |
| [Issue 76](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=76) | Documentation | Medium | Document that if Selenium Server is restarted it may need to use different port |
| [Issue 82](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=82) | Documentation | Medium | Documentation enhancement do describe how to handle self signed certificates |
| [Issue 41](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=41) | Enhancement | Low | Remove deprecated `Shut Down (Selenium) Server` -> `Stop Selenium Server` |
| [Issue 91](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=91) | Enhancement | Low | Support for absolute paths as a custom location for `Capture Screenshot` |

Altogether 25 issues.