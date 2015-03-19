

# Introduction #

The default Firefox profile is not very automation friendly, and thus SeleniumLibrary 2.5 and newer use a customized profile by default. Instructions below also explain how to create your own custom profile and how to take it into use. One good use case for a custom profile is [handling self-signed certificates](HandlingSelfSignedCertificates.md).

# Profile distributed with SeleniumLibrary #

Starting from [SeleniumLibrary 2.5](ReleaseNotes25.md), the library itself ships a custom Firefox profile that it uses by default. This profile turns both the offline mode and proxy off (how to do that yourself is explained below), and it also removes unnecessary toolbars and other clutter from the user interface. The profile files are contained in the installation in `<installation-path>/SeleniumLibrary/firefoxprofile` and they can also be viewed [online](http://robotframework-seleniumlibrary.googlecode.com/hg/src/SeleniumLibrary/firefoxprofile/).

If you have ideas for further customization, please submit an [enhancement request](http://code.google.com/p/robotframework-seleniumlibrary/issues/list).

# Creating custom profile #

Execute command `firefox -ProfileManager` on the command line and choose a sane directory for the profile. Notice that you cannot have Firefox running when you run this command.

[This page](http://girliemangalo.wordpress.com/2009/02/05/creating-firefox-profile-for-your-selenium-rc-tests/), and many others, contains lots of useful customizations. Here are a couple of additional ones that have been found useful:

  * Enable running tests on `localhost` even when network is not available (works only with Firefox 3.6 and newer):
    * Open `about:config` using the test profile
    * Right click and choose `New | Boolean`
    * Enter `network.manage-offline-status` as name and set value to false
  * Force proxy off:
    * Open `about:config using` the test profile
    * Right click and choose `New | Integer`
    * Enter `"network.proxy.type"` as name and set value to 3

After the profile has been created, there are bunch of files (and some subdirectories) in the custom profile directory. Most of the important content is in `prefs.js`, and view related content such as visible toolbars are stored in `localstore.rdf`. All other files and subdirectories can be removed. This is useful if you want to put the profile in version control, for example.

# Taking custom profile into use #

The Firefox profile to use must configured using `-firefoxProfileTemplate` option given to Selenium Server when it is started. For example, if you use `Start Selenium Server` keyword provided by the library, you need to use something like this:

| Start Selenium Server | -firefoxProfileTemplate | /path/to/the/profile |
|:-----------------------|:------------------------|:---------------------|

When using SeleniumLibrary to start up the Selenium Server, this option also overrides the [profile distributed with the library](#Profile_distributed_with_SeleniumLibrary.md). If you start the Selenium Server otherwise, setting the custom profile is always on your responsibility.

If you want to use the default Firefox profile on your machine instead of the one distributed with the library, but do not want to create a custom profile yourself, you need to use a special value `DEFAULT` with the `-firefoxProfileTemplate` option. This should not be needed unless you have done customization to your machine's default profile.

| Start Selenium Server | -firefoxProfileTemplate | DEFAULT |
|:----------------------|:------------------------|:--------|