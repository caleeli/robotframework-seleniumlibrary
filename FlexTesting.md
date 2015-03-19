

# Introduction #

This page explains how to use SeleniumLibrary to run tests against Adobe Flex applications. Although it has not been explicitly tested, it should be possible to test also Flash applications the same way.

The Flex testing support was added in [SeleniumLibrary 2.6](ReleaseNotes26.md). It is internally implemented using [Flex Pilot](http://github.com/mde/flex-pilot) tool and it requires applications to be bootstrapped as explained in the next section. Both Flex 3 and Flex 4 based applications are supported.

The [SeleniumLibrary demo](Demo.md) has been updated to include an example Flex application with required bootstrapping. The tests and higher level keywords the demo contains can also be used as an example how to create easy-to-maintain automated test cases for Flex applications.

# Bootstrapping #

The tested application needs to be modified a bit so that it bootstraps Flex Pilot tool. In practice this is done by importing and initializing `FPBootstrap` package that you need to download separately. How the actual bootstrapping code looks like depends on whether the application is written in MXML or ActionScript.

## Getting `FPBootstrap` ##

The easiest way to get the needed `FPBootstrap` package is downloading `FPBootstrap.zip` from the [Flex Pilot download page](http://github.com/mde/flex-pilot/downloads) and extracting it. Alternatively you can checkout the [Flex Pilot source code](https://github.com/mde/flex-pilot).

## Bootstrapping in MXML ##

The application needs to be changed so that the bootstrapping code is loaded when the application is otherwise initialized. An easy way to accomplish this is binding the bootstrap to `applicationComplete` attribute of the top-level `<mx:Application>` tag:

```
<mx:Application xmlns:mx="http://www.adobe.com/2006/mxml" layout="absolute" applicationComplete="bootstrapFlexPilot();">
<mx:Script>
<![CDATA[
  // Import and initialize Flex Pilot bootstrapper
  import org.flex_pilot.FPBootstrap;
  private function bootstrapFlexPilot():void {
    FPBootstrap.flex_pilotLibPath = 'FlexPilot.swf';
    FPBootstrap.init(stage);
  }
]]>
</mx:Script>
<mx:Label id="example" text="Normal application code here" />
</mx:Application>
```

For an executable example see the simple [Login Application](http://robotframework-seleniumlibrary.googlecode.com/hg/demo/demoapp/flex) that is included into the [SeleniumLibrary demo](Demo.md).

## Bootstrapping in ActionScript ##

The following code needs to be added into the application code after the application's stage has been initialized:

```
  import org.flex_pilot.FPBootstrap;
  FPBootstrap.flex_pilotLibPath = 'FlexPilot.swf';
  FPBootstrap.init(stage);
```

## Compiling ##

When the bootstrapping code is in place, the application needs to be recompiled so that the `FPBootstrap` package is in the source path. You can do that from the command prompt like below:

```
mxmlc -source-path=<ApplicationSourceDir> -source-path +=<FPBootstrapDir> path/to/your/Application.mxml
```

In the above command `<FPBootstrapDir>` is the directory where you extracted `FPBootstrap.zip` to or checked out Flex Pilot `src` directory. If you use Flash Builder or some other IDE, you need to add the same directory into the source path before compilation.

After the compilation you can use [Firebug](#Firebug.md) to verify has the bootstrapping been successful.

# Runtime dependencies #

## Flex Pilot: `FlexPilot.swf` ##

The Flex Pilot tool itself has been compiled into `FlexPilot-<version>.swf` package. There are separate Flex 3 and Flex 4 compatible versions and both of them are available on the [Flex Pilot download page](https://github.com/mde/flex-pilot/downloads). Flex Pilot documentation also contains instructions on how to compile it yourself if you have special needs.

The bootstrapping code loads Flex Pilot dynamically. When the bootstrapping is done like in the examples above, you need to copy `FlexPilot.swf` into the application server into the same directory as the application's own `.swf` file. If you want to put `FlexPilot.swf` into some other directory or use different name, you need to change line `FPBootstrap.flex_pilotLibPath = 'FlexPilot.swf';` in the bootstrap code accordingly.

## Selenium: `user-extensions.js` ##

Integrating Flex Pilot with Selenium requires starting Selenium Server with special user extensions file. When using `Start Selenium Server` keyword or `start_selenium_server` function provided by the library, these extensions are loaded automatically.

If you start Selenium Server otherwise, you need to register the same [user-extensions.js](http://robotframework-seleniumlibrary.googlecode.com/hg/src/SeleniumLibrary/lib/user-extensions.js) file with `-userExtensions` option. Notice that because Selenium Server only supports one user extension file, you need to combine files together if you want to use also some other extensions.

# Provided keywords #

All the Flex related keywords are listed in the [library documentation](LibraryDocumentation.md) and they all have `Flex` in their name. Notice that you always need to use `Select Flex Application` keyword before you can use other Flex keywords.

# Debugging #

## Firebug ##

It is possible to use [Firebug](https://addons.mozilla.org/en-US/firefox/addon/1843/) tool to execute Flex Pilot commands interactively. Being able to run commands this way proves that Flex Pilot bootstrapping has succeeded. Once the application has been opened in the browser, Flex Pilot commands can be executed in the Firebug console like this:

```
document.getElementById('appId').fp_click({'id': 'elemId'})
```

In the above example `appId` is the id of the Flex Application in the HTML source code and `elemId` is the id of the clicked element in the Flex source. All the available Flex Pilot commands and their arguments are listed in the [Flex Pilot API](https://github.com/mde/flex-pilot/wiki/api).

If you just want to verify that bootstrapping works, you can run only the example below. Everything should be set up correctly if this command returns `function`, `fp_click()` or something similar. If you get `undefined`, you need to checkout your bootstrapping again.

```
document.getElementById('appId').fp_click
```

## Debug Flash player ##

It is strongly recommended to install [debug version](http://www.adobe.com/support/flashplayer/downloads.html) of the Flash
player from Adobe when testing Flex/Flash applications. The player
should be also configured to log error messages as per [these instructions](http://livedocs.adobe.com/flex/3/html/help.html?content=logging_04.html).

## Debug log level ##

The library logs some more information about the underlying Selenium commands it executes using debug log level. To see these messages, you need to run tests with option `--loglevel DEBUG`.