# Introduction #

These instructions explain how to create a custom Firefox profile to test pages using https and self-signed certificates. See CustomFirefoxProfile wiki page for more information about custom profiles.

The solution is copied from
http://townx.org/blog/elliot/dealing-self-signed-ssl-certificates-when-running-selenium-server-firefox

# Create custom Firefox profile #

  1. Close down any running Firefox instances.
  1. Start Firefox (the one you're going to run your tests with) with the profile manager: firefox -ProfileManager
  1. Create a new profile. You'll be prompted to choose a directory for the profile. Put it somewhere inside the project where you're writing the tests.
  1. Select the profile and run Firefox using it.
  1. Browse to the HTTPS URL (with self-signed certificate) you're going to be testing against.
  1. Accept the self-signed certificate when prompted. This creates an exception for it in the profile.
  1. Close the browser.
  1. Go to the Firefox profile directory.
  1. Delete everything in the directory except for the cert\_override.txt and cert8.db files.
  1. When you run your Selenium server pass a -firefoxProfileTemplate /path/to/profile/dir argument to it. This tells Selenium to use your partial profile (with certificate exceptions) as a basis for minting its new profile. So you get the certificate exceptions, but without any of the other clutter you would get if you used a whole profile.

# Example test #
```
***Settings***
Library     SeleniumLibrary

***Test Case***
Example
    Start Selenium Server  -firefoxProfileTemplate  /home/xx/firefoxprofile
    Open Browser  https://1.2.3.4/hostedOffice
```