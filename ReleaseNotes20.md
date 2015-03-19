# Release Notes #

This page contains release notes for Selenium Library 2.0 series.

## Selenium Library 2.0 ##

Version 2.0 is the first open source release of Selenium Library for Robot Framework.
The LibraryDocumentation lists the available keywords.

## Selenium Library 2.0.1 ##

  * Aliases ie and ff have been added to Open Browser and the keyword documentation has been improved([issue4](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=4))
  * Optional argument wait has been added to keyword Select Radio Button. This is needed to operate radio buttons whose actions cause a page load.


## Selenium Library 2.0.2 ##

This release adds support for popup windows and fixes problem with button tag.
The documentation is also greatly improved.

| **ID** | **Type** | **Priority** | **Summary** |
|:-------|:---------|:-------------|:------------|
| [Issue 6](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=6) | Defect | High | Click Button does not work with 

&lt;button&gt;

 tag |
| [Issue 7](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=7) | Documentation | High | Documentation enhancements |
| [Issue 9](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=9) | Defect | Medium | Cannot select and test Modal Dialogues. When popup test is frozen |