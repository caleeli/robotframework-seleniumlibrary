

# Introduction #

The `SeleniumLibrary` has a number of unit and acceptance tests that are used to verify that the library can be taken into use successfully and the keywords it provides work properly.

The tests and related resources are located under `test` directory in the
[source tree](http://code.google.com/p/robotframework-seleniumlibrary/source).
That directory contains everything needed to run the tests, including:

  * Robot Framework test case files, which can be found under `acceptance` directory.
  * Some unit tests under `unit` directory
  * A collection of simple HTML files under `resources/html` directory, used as test data.
  * A very simple web server (`resources/testserver/httpserver.py`), which is used to serve the HTML files for tests.
  * Start-up script `run_tests.py` for executing the tests.

# Running tests #

The start-up script runs first the unit tests and if those pass, then runs the RF tests. It may be used to execute the tests like this:

```
   python run_tests.py python|jython browser [options]
```

The first argument to the scrip defines the interpreter to be used
to run Robot Framework and the second argument specifies the browser to be used.
Browser is any browser or alias accepted by SeleniumLibrary. Notice that the start-up script itself should always be executed using Python.

Due to the structure of the tests, the top-level directory containing the test
case files is always given to Robot Framework as test data path.
Command line options `--test`, `--suite`, `--include` and `--exclude` can be used
to run only a subset of test cases.

## Examples ##

```
  # Run all test with Python and Firefox
  python run_tests.py python ff
  # Run only test suite `javascript` with Jython and Internet Explorer
  python run_tests.py jython ie --suite javascript
```


# Failing tests #

When the tests are executed, a number of test cases can be seen to
fail in the console output.  This is because these "negative" test cases are
designed to test that the keywords fail with correct error messages.
After the execution, [statuschecker.py](http://code.google.com/p/robotframework/wiki/TestStatusCheckerTool) script is used to verify these errors, and also log messages, based on test cases' documentation. After that, report and log files are
generated, and these files show the correct status of the test run. The overall status is also printed as the last statement to the console.


# Known issues #

Some of the tests fail with Internet Explorer, because it handles
xpath expressions a little differently than Firefox. This is an issue
that should be handled in the library, but the implementation is not
there yet.