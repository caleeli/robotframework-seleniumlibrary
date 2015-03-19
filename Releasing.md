

Creating SeleniumLibrary release requires following steps. The commands mentioned should be executed from the project root.

# Run acceptance tests #

Run AcceptanceTests on different operating systems, with Python and Jython, and with different browsers. The exact combination of platforms and browsers that should pass is not yet defined.

# Create release tag #

  * Update your local repository with command `hg pull -u`
  * Update version in file `src/SeleniumLibrary/version.py`
  * Create library documentation with command `python doc/generate.py`
  * Commit changes to local repository, do not push yet.
  * Create Mercurial tag with command `hg tag <version>` (e.g. `hg tag 2.5.1`)
  * Push changes to the central repository, this will also push the tag information

# Create packages #

  * Update to the release tag with `hg pull && hg update <version>` (if not creating package on the same machine where the tag was created)
  * Make sure you don't have extraneous files in your working directory with command `hg status`
  * Create source distribution (on Linux/OSX machine) with command `python setup.py sdist`
  * Create 32 and 64 bit Windows installer (on a matching Windows machine) with command `python setup.py bdist_wininst`
  * Upload the distributions to [download page](http://code.google.com/p/robotframework-seleniumlibrary/downloads/list)
  * Upload the distributions to NSN's internal download page

# Write release notes #

  * Generate list of issues with [get\_issues.py](http://robotframework.googlecode.com/svn/wiki/tools/get_issues.py) script. Common usage is `get_issues.py notes seleniumlibrary 2.5.1 >> ReleaseNotes25.wiki`.
  * For major releases add free text describing the biggest new features/fixes, backwards incompatible changes (if any), acknowledgments, etc. See e.g. ReleaseNotes25 for an example.
  * Minor releases can be added into the same page as major releases.

# Reset version in head #

  * Set version in `src/SeleniumLibrary/version.py` to `devel` (or something similar)
  * Commit and push

# Announce release #

  * Insert link to latest documentation version in LibraryDocumentation
  * Add news to SeleniumLibrary and Robot Framework project front pages
  * Update [PyPI](http://pypi.python.org/pypi/robotframework-seleniumlibrary).
  * Send a release mail
  * Advertise release on Twitter and elsewhere
  * Drink sparkling