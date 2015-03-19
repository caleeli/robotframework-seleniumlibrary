

# SeleniumLibrary 2.5 #

When the development of this SeleniumLibrary release started, it was labeled 2.4.1 and the idea was to just have a quick bug fix release for the [previous](ReleaseNotes24.md) release. In the end the amount of new keywords and other exciting new functionality made it clear that this release deserves label 2.5.

SeleniumLibrary 2.5 was released on Tuesday 2010-11-16. The installers are available on the [download page](http://code.google.com/p/robotframework-seleniumlibrary/downloads/list).

# Most important features #

## Automatic screenshot on failure ##

The library will automatically take a screenshot whenever another keyword from the library fails. It is possible to use also some other action or disable this feature altogether. For more information see [issue 139](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=139) and the Importing section in the [library documentation](LibraryDocumentation.md).

## Custom Firefox profile ##

The library uses a custom Firefox profile with automation friendly customization. For more information see [issue 151](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=151) and a [separate wiki page](CustomFirefoxProfile.md) that explains also how to use your own custom profiles.

## Installation via `easy_install` ##

It is possible to install SeleniumLibrary with Python's [easy\_install](http://packages.python.org/distribute/easy_install.html) package management tool ([issue 143](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=143)). If you have `easy_install` installed, all you need to do is run command `easy_install robotframework-seleniumlibrary`.

## Lot of new keywords ##

This release contains altogether 10 new keywords. See the list of issues below for details.

# Backwards incompatible changes #

A consequence of using a custom Firefox profile by default is that possible customization in the system default profile are not taken into account. The wiki page [explaining custom profiles](CustomFirefoxProfile.md) also explains how to force using the default profile.

# Acknowledgments #

Big thanks for Robert Spielmann from [codecentric](http://www.codecentric.de) for implementing, with tests and documentation, several new keywords ([issue 118](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=118), [issue 136](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=136), [issue 137](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=137), [issue 144](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=144)), and helping with documentation ([issue 127](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=127), [issue 140](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=140)) and other tasks. Robert has been awarded with commit rights and is now considered one of the core developers of this library.

Additional thanks for user xieyanbo for great patch for [issue 138](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=138), and for the.real.pjeby for a tip how to resolve the `easy_install` bug ([issue 143](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=143)).

# List of all fixes and enhancements #

| **ID** | **Type** | **Priority** | **Summary** |
|:-------|:---------|:-------------|:------------|
| [Issue 143](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=143) | Defect | High | Installation using Python's `easy_install` does not work |
| [Issue 139](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=139) | Enhancement | High | Take screenshot automatically on failure (and also allow using other actions) |
| [Issue 151](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=151) | Enhancement | High | Use independent Firefox profile with SeleniumLibrary by default |
| [Issue 118](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=118) | Enhancement | Medium | New `Mouse Over`, `Mouse Out`, `Mouse Down`, and `Mouse Up` keywords |
| [Issue 122](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=122) | Enhancement | Medium | `Execute Javascript` keyword should support executing JS file directly |
| [Issue 136](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=136) | Enhancement | Medium | New `Xpath Should Match X Times` keyword |
| [Issue 137](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=137) | Enhancement | Medium | New `Element Text Should Be`  keyword |
| [Issue 138](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=138) | Enhancement | Medium | `Confirm Action` keyword should return the message of javascipt confirmation  |
| [Issue 142](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=142) | Enhancement | Medium | New `Get List Items` keyword |
| [Issue 144](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=144) | Enhancement | Medium | New `Element Should (Not) Be Visible` keywords |
| [Issue 146](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=146) | Enhancement | Medium | New `Wait Until Page Loaded` keyword |
| [Issue 147](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=147) | Enhancement | Medium | `Page Should (Not) Contain` keywords should support disabling logging page source on failure |
| [Issue 149](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=149) | Documentation | Medium | Instructions to create custom Firefox profile |
| [Issue 148](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=148) | Defect | Low | `Page Should Not Contain` keyword does not go through frames similarly as `Page Should Contain` |
| [Issue 131](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=131) | Enhancement | Low | Update Selenium Python API (selenium.py) to the latest version |
| [Issue 154](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=154) | Enhancement | Low | Add more aliases for `Open Browser` |
| [Issue 127](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=127) | Documentation | Low | Typo in the docs |
| [Issue 140](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=140) | Documentation | Low | Documentation of radio button related keywords doesn't explain how the buttons are located |
| [Issue 141](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=141) | Documentation | Low | Document that `(Un)Select From List` need to use new `Wait Until Page Loaded` keyword if waiting page load needed |

Altogether 19 issues.