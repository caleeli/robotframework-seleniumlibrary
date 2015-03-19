

# Introduction #

The latest release is always available in the [downloads](http://code.google.com/p/robotframework-seleniumlibrary/downloads/list).
`SeleniumLibrary` distribution contains the actual library code,
the [Selenium Server](http://seleniumhq.org/projects/remote-control/) as a JAR package, and Selenium Python bindings that the library uses to communicate with the server.
See [architecture page](Architecture.md) for more information about the different components
and the [demo](Demo.md) for example test cases.

# Preconditions #

The Selenium Server requires Java runtime version 1.5 or newer.

The `SeleniumLibrary` itself supports all Python and Jython versions that are supported by Robot Framework.

# Installing from source #

The source code can be got either as a source distribution or as a checkout from our version control system. The installer requires Python version 2.4 or newer.
Selenium Library is installed from source by typing following command:

```
    python setup.py install
```

In most Unixy systems, you need to have root privileges for installation.

Uninstallation is achieved by deleting the installation directory and its contents from the file system. The default installation directory is `[PythonLibraries]/site-packages/SeleniumLibrary`.

# Using Windows installer #

It is enough to double-click the installer and follow the instructions.

Selenium Library can be uninstalled using Add/Remove Programs utility from Control Panel.

# Provided keywords #

Keywords provided by the `SeleniumLibrary` are listed in separate version specific [library documentations](LibraryDocumentation.md).

# Starting Selenium Server #

After a normal installation library can be taken into use without further configuration, but the Selenium Server must be started before the keywords can be used. The easiest way to start and stop the server distributed with the library is using `Start Selenium Server` and `Stop Selenium Server` [keywords](LibraryDocumentation.md).

It is also possible to the server it before test execution either manually or automatically so that different test suites don't need to control it at all.
To start the server included with the library you can run command
similar to the example below. `[PythonLibraries]` is typically something like `/usr/lib/python2.6` or `C:\Python26\Lib`, depending on the platform and the installed Python version.

```
    java -jar [PythonLibraries]/site-packages/SeleniumLibrary/lib/selenium_server.jar
```

It is also possible to use other Selenium Servers, for example newer version than the one distributed with the library, or copy the distributed version into some other machine. In these cases the server must always be started before test execution.

See [Selenium documentation](http://seleniumhq.org/docs/) for more information about
the Selenium Server, different command line options it accepts, and the Selenium Remote Controller (RC) concept in general.