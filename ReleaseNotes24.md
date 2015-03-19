

# SeleniumLibrary 2.4 #

SeleniumLibrary 2.4 was released 2010-05-27.

This release started out as a bug fix release, targeting a fix for [issue 107](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=107). But while working on it, the team found that it should address also some other problems and ended up with many new features that made their way into this release, notably the new table related keywords a new way to upload files.

## Acknowledgments ##

Andreas Ebbert-Karroum has made major contributions to this release and as a consequence of that, has been promoted to an owner of the SeleniumLibrary project. No more special acknowledgements after this release for you Andreas :)

Thanks also to Radek Wierzbicki for implementing support for remote files when using `Choose File` keyword ([issue 108](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=108))

Thanks to everyone who has submitted enhancement requests and bug reports.


## List of all fixes and enhancements ##

| **ID** | **Type** | **Priority** | **Summary** |
|:-------|:---------|:-------------|:------------|
| [Issue 107](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=107) | Defect | High | Handling errors when the message contains Unicode characters fails on Python/Jython < 2.6 |
| [Issue 27](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=27) | Enhancement | High | Keywords for checking and getting table content |
| [Issue 110](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=110) | Enhancement | High | Switch version control from Subversion to Merqurial |
| [Issue 114](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=114) | Enhancement | High | Support Firefox 3.6 |
| [Issue 95](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=95) | Defect | Medium | Clicking a link inside frame does not work in IE |
| [Issue 109](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=109) | Defect | Medium | `Go Back` keyword should wait until page is loaded |
| [Issue 108](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=108) | Enhancement | Medium | Support for using remote files with `Choose File` |
| [Issue 117](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=117) | Enhancement | Medium | Add Link to Selenium Documentation in API-Documentation for Keyword CallSeleniumApi |
| [Issue 97](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=97) | Documentation | Medium | Document that opening multiple browsers does not work with IE |
| [Issue 105](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=105) | Defect | Low | Improve `Element Should Contain` fail message |
| [Issue 96](https://code.google.com/p/robotframework-seleniumlibrary/issues/detail?id=96) | Documentation | Low | Document that `Press Key` does not work with IE |

Altogether 11 issues.