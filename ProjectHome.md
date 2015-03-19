# SeleniumLibrary #

SeleniumLibrary is a [Robot Framework](http://robotframework.org) test library that uses the popular [Selenium](http://seleniumhq.org) web testing tool internally. It provides a powerful combination of simple test data syntax and support for [different browsers](http://seleniumhq.org/about/platforms.html#browsers). In addition to standard web testing, the library also supports [testing Adobe Flex/Flash applications](FlexTesting.md).

See the _**[SeleniumLibrary demo](Demo.md)**_ for executable example test cases and reports,
look at the [library documentation](LibraryDocumentation.md) for information about the provided keywords, and consult the [installation instructions](InstallationInstructions.md) if you want to use the library yourself.

## Selenium 1 vs. Selenium 2 ##

SeleniumLibrary internally uses [Selenium Remote Controller API](http://seleniumhq.org/projects/remote-control/) that is part of Selenium 1. If you want to use the new [Selenium 2 WebDriver API](http://seleniumhq.org/projects/webdriver/), you should look at [Selenium2Library](https://github.com/rtomac/robotframework-selenium2library) that is, for most parts, a drop-in-replacement for SeleniumLibrary.

According to http://seleniumhq.org, the old Remote Controller API is officially deprecated in favor of the new WebDriver API. As a result also _**SeleniumLibrary is deprecated**_ and no new releases are expected. New users should use the already mentioned [Selenium2Library](https://github.com/rtomac/robotframework-selenium2library) and existing users should start to plan migrating to it.

## Videos ##

[Elisabeth Hendrickson](http://testobsessed.com/) demonstrating Robot Framework and SeleniumLibrary at [Selenium Testing Tools Demo Night](http://saucelabs.com/blog/index.php/2010/04/highlights-from-our-april-20th-selenium-testing-tools-demo-night/):

<a href='http://www.youtube.com/watch?feature=player_embedded&v=qf2i-xQ3LoY' target='_blank'><img src='http://img.youtube.com/vi/qf2i-xQ3LoY/0.jpg' width='425' height=344 /></a>

## News ##

  * _2012-08-28_ **[SeleniumLibrary 2.9.1](ReleaseNotes29.md)** released with Selenium Server 2.21.
  * _2012-05-08_ **[SeleniumLibrary 2.9](ReleaseNotes29.md)** released with Selenium Server 2.21.
  * _2011-12-19_ **[SeleniumLibrary 2.8.1](ReleaseNotes28#SeleniumLibrary_2.8.1.md)** released with support for Firefox 8 via Selenium server 2.15.
  * _2011-10-22_ The first version of **[Selenium2Library](https://github.com/rtomac/robotframework-selenium2library)**, a drop-in-replacement for SeleniumLibrary using [Selenium 2 WebDriver API](http://seleniumhq.org/projects/webdriver/), has been released.
  * _2011-08-09_ **[SeleniumLibrary 2.8](ReleaseNotes28.md)** released with support for Firefox 5 via Selenium server 2.3.
  * _2011-05-02_ **[SeleniumLibrary 2.7](ReleaseNotes27.md)** released with support for Firefox 4 and some new keywords.
  * _2011-01-31_ **[SeleniumLibrary 2.6](ReleaseNotes26.md)** released with [Flex testing support](FlexTesting.md) and various other fixes and features.
  * _2011-01-31_ **[Demo](Demo.md)** updated with Flex version of the demo application and tests.
  * _2010-11-16_ **[SeleniumLibrary 2.5](ReleaseNotes25.md)** is released with lot of new keywords, automatic screenshots on failures, and other enhancements.
  * _2010-05-27_ **[SeleniumLibrary 2.4](ReleaseNotes24.md)** is released.
  * _2010-05-05_ **[Architecture](Architecture.md)** documented
  * _2010-04-28_ **[Demo](Demo.md)** enhanced
  * _2010-03-10_ **[SeleniumLibrary 2.3.1](ReleaseNotes23.md)** is released.
  * _2010-02-15_ **[SeleniumLibrary 2.3](ReleaseNotes23.md)** is released.
  * _2009-11-30_ **[SeleniumLibrary 2.2.2](ReleaseNotes22.md)** is released.
  * _2009-08-24_ **[SeleniumLibrary 2.2.1](ReleaseNotes22.md)** is released.
  * _2009-05-14_ **[SeleniumLibrary 2.2](ReleaseNotes22.md)** is released.
  * _2009-02-02_ **[SeleniumLibrary 2.1.2](ReleaseNotes21.md)** is released.
  * _2009-01-15_ **[SeleniumLibrary 2.1.1](ReleaseNotes21.md)** is released.
  * _2008-12-05_ **[SeleniumLibrary 2.1](ReleaseNotes21.md)** is released.
  * _2008-10-20_ **[SeleniumLibrary 2.0.2](ReleaseNotes20.md)** is released.