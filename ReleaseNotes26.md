

# SeleniumLibrary 2.6 #

The absolutely biggest new feature in SeleniumLibrary 2.6 is the support for testing [Flex and Flash applications](FlexTesting.md) ([issue 31](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=31)). That alone would have been more than enough for a new major release, but there are also several important fixes and nice features for "normal" web testing.

SeleniumLibrary 2.6 was released on Monday 2011-01-31. The installers are available on the [download page](http://code.google.com/p/robotframework-seleniumlibrary/downloads/list) and normal [installation instructions](InstallationInstructions.md) apply.

# Acknowledgments #

Bastian helped us to understand why connection error messages from Jython were so poor ([issue 156](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=156)) which allowed to workaround the problem. He also reported the underlying bug into [Jython's issue tracker](http://bugs.jython.org/issue1697) and it has already been fixed.

Big thanks also to Mika Batsman for reporting problem with operating `<button>`s ([issue 157](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=157)) and providing great patch to it.

# List of all fixes and enhancements #

| **ID** | **Type** | **Priority** | **Summary** |
|:-------|:---------|:-------------|:------------|
| [Issue 31](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=31) | Enhancement | Critical | Support for Flex and Flash |
| [Issue 155](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=155) | Defect | High | `Go To` keyword causes XHR error with Firefox |
| [Issue 171](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=171) | Defect | High | Two Firefox windows are opened when tests are run with the included profile |
| [Issue 160](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=160) | Enhancement | High | Upgrade Selenium Server 2.0 beta 1 (to fix e.g. `Delete All Cookies`) |
| [Issue 170](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=170) | Enhancement | High | Update demo to contain Flex examples and otherwise |
| [Issue 156](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=156) | Defect | Medium | On Jython connecting to Selenium Server on localhost can fail without retrying and with bad error message |
| [Issue 157](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=157) | Defect | Medium | Operating buttons created with `<button>` tag using visible text is not possible |
| [Issue 164](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=164) | Defect | Medium | `Wait Until Page Loaded` requires timeout to be number in milliseconds |
| [Issue 172](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=172) | Defect | Medium | `Radio Button Should Be Set To` and `Radio Button Should Not Be Selected` report failures incorrectly with IE8 |
| [Issue 158](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=158) | Enhancement | Medium | Table keywords should accept table locator as XPath too |
| [Issue 161](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=161) | Enhancement | Medium | All `Wait Until ...` keywords should use Selenium timeout by default |
| [Issue 163](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=163) | Enhancement | Medium | New `Element Should Be Enabled/Disabled` keywords |
| [Issue 167](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=167) | Enhancement | Low | `Get Window Names/Titles/Identifiers` should log what it returns |

Altogether 13 issues.