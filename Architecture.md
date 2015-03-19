

![http://wiki.robotframework-seleniumlibrary.googlecode.com/hg/architecture.png](http://wiki.robotframework-seleniumlibrary.googlecode.com/hg/architecture.png)

# Test data #

The test data contains the actual test cases and possible resource files
needed by them. These files must be in format understood by Robot Framework.

# Robot Framework #

[Robot Framework](http://robotframework.org) is a generic test
automation framework that uses different test libraries to interact
with the applications under test.

# SeleniumLibrary #

`SeleniumLibrary`, as you probably know if you are reading this
documentation, is a web testing library for Robot Framework. As the name
implies, it uses popular [Selenium](http://seleniumhq.org) web
testing tool internally. When the library is used for [Flex testing](FlexTesting.md) it uses also [Flex Pilot](https://github.com/mde/flex-pilot) tool.

The `SeleniumLibary` uses
[Selenium Remote Controller's](http://seleniumhq.org/projects/remote-control/)
(RC) Python client library to communicate with the Selenium Server.

# Selenium Server #

The Selenium Server is the core component of the
[Selenium Remote Controller](http://seleniumhq.org/projects/remote-control/).
It is responsible on launching browsers and interacting
with them. It is a Java application, but there are client libraries
for various programming languages. Using these bindings requires that
the Selenium Server is running.

As explained in the [installation instructions](InstallationInstructions.md),
the `SeleniumLibrary` includes the Selenium Server JAR package. The
installation instructions also explain how to the server is
[started and stopped](InstallationInstructions#Starting_Selenium_Server.md).

# Browsers #

Probably the best feature of the Selenium tool is that it supports various
different browsers. See the [Open Browser](LibraryDocumentation.md) keyword for
more information on how to use different browsers with the `SeleniumLibrary`
and [Selenium documentation](http://seleniumhq.org/docs/) for a full list
of supported browsers.

To easily run tests with different browsers, it is generally a good idea to specify the browser that the `Open Browser` keyword with a variable in the test data. This functionality is demonstrated well by the [SeleniumLibrary demo](Demo#Using_different_browsers.md).

# System Under Test #

The most important component is obviously the web application you are testing.