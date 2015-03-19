

# Introduction #

This pages features a quick how-to on replacing the on-board Selenium Server that comes with SeleniumLibary with Selenium GRID. This allows to automatically distribute tests to multiple systems (e.g. to test different browser environments) or to allow parallel execution of tests to shorten the execution time.

# Use Selenium GRID instead of Selenium Server #

Stop using all Selenium Server related keywords in your tests, `Start Selenium Server` and `Stop Selenium Server` are not able to control Selenium GRID.

Check the spots where you import SeleniumLibrary, server and port (server\_host=localhost, server\_port=4444) need to match with the Selenium GRID hub you'll start later. Note that if you import SeleniumLibrary without additional parameters and plan to start the hub on the same machine as the tests you don't need to change anything. It is also a good idea to specify server and port using variables, this way the can be passed to via command line to individual `pybot` instances. So a good import looks like this:

| Setting | Value | Value | Value | Value |
|:--------|:------|:------|:------|:------|
| Library | SeleniumLibray |	15.0 | ${SELENIUM HOST} | ${SELENIUM PORT} |

Or this if you use Robot Framework 2.5 which supports named arguments:

| Setting | Value | Value | Value |
|:--------|:------|:------|:------|
| Library | SeleniumLibray |	server\_host=${SELENIUM HOST} | server\_port=${SELENIUM PORT} |

Parametrize every usage of the `Open Browser` keyword to use a fixed global variable for the `browser` parameter, this way the variable can be passed to individual `pybot` instances via command line, for example:

| Open Browser | http://www.robotframework.org | ${BROWSER} |
|:-------------|:------------------------------|:-----------|

Assuming you have set up Selenium GRID as described [here](http://selenium-grid.seleniumhq.org/get_started.html), open a command prompt and navigate to the installation directory. Start a hub:

```
ant launch-hub
```

Note this will start the GRID on port 4444 per default, if you specify an other port here make sure to also specify the same port when importing SeleniumLibrary in your tests.
Open another command prompt to start a remote control:

```
ant -Dport=5558 -Dhost=127.0.0.1 -DhubURL=http://127.0.0.1:4444 -Denvironment="*firefox" launch-remote-control
```

**Note:** For `-Denvironment` use whatever browser you like the remote control to use, make sure to use the same string in the `Open Browser` keyword, or in the global `${BROWSER}` variable as described above. To start multiple remote controls the `-Dport` value needs to be different for every remote control.

Now go ahead and start your tests, assuming you have replaced the selenium host / port and the browser specification in your tests, the command will look like this:
```
pybot --variable "SELENIUM_HOST:127.0.0.1" --variable "SELENIUM_PORT:4444" --variable "BROWSER:*firefox" path/to/tests
```

# Distribute Tests to Different Browsers #

Let's assume you want to run the same test suite vs Internet Explorer and Firefox, with the settings from above your commands to start up your tests will look like this:

Start the hub:
```
ant launch-hub
```

Start remote control for Internet Explorer:
```
ant -Dport=5558 -Dhost=127.0.0.1 -DhubURL=http://127.0.0.1:4444 -Denvironment="*iexplore" launch-remote-control
```

Start remote control for Firefox:
```
ant -Dport=5559 -Dhost=127.0.0.1 -DhubURL=http://127.0.0.1:4444 -Denvironment="*firefox" launch-remote-control
```

Start `pybot` to run tests with Internet Explorer:
```
pybot --variable "SELENIUM_HOST:127.0.0.1" --variable "SELENIUM_PORT:4444" --variable "BROWSER:*iexplore" -o outputIE.xml -l logIE.xml -r reportIE.html path/to/tests
```

Start `pybot` to run tests with Firefox:
```
pybot --variable "SELENIUM_HOST:127.0.0.1" --variable "SELENIUM_PORT:4444" --variable "BROWSER:*firefox" -o outputFF.xml -l logFF.xml -r reportFF.html path/to/tests
```

Note that the two `pybot` instances can run in parallel without any problem. In the example I specified explicit output, log and report files for the two runs, otherwise they will use the default file names and interfere with each other resulting in non-usable logs. You can use the `rebot` tool to merge the results later if desired.

# Run Test Suites in Parallel #

Running tests from different suites is pretty simple. Of course you got to make sure that the tests you are executing in parallel have no potential of disturbing each other (e.g. if a test shut down the application, some other tests might fail because the application is not running). The start-up command are almost similar to the ones above:

Start the hub:
```
ant launch-hub
```

Start some remote controls:
```
ant -Dport=5558 -Dhost=127.0.0.1 -DhubURL=http://127.0.0.1:4444 -Denvironment="*firefox" launch-remote-control
ant -Dport=5559 -Dhost=127.0.0.1 -DhubURL=http://127.0.0.1:4444 -Denvironment="*firefox" launch-remote-control
ant -Dport=5560 -Dhost=127.0.0.1 -DhubURL=http://127.0.0.1:4444 -Denvironment="*firefox" launch-remote-control
```

**Note:** The remote controls can, of course, be distributed to different machines or virtual machines. The more RCs you have, the faster your tests will be done.

Start `pybot` instances for the different suites:
```
pybot --variable "SELENIUM_HOST:127.0.0.1" --variable "SELENIUM_PORT:4444" --variable "BROWSER:*firefox" -o output-A.xml -l log-A.xml -r report-A.html path/to/tests/a
pybot --variable "SELENIUM_HOST:127.0.0.1" --variable "SELENIUM_PORT:4444" --variable "BROWSER:*firefox" -o output-B.xml -l log-B.xml -r report-B.html path/to/tests/b
pybot --variable "SELENIUM_HOST:127.0.0.1" --variable "SELENIUM_PORT:4444" --variable "BROWSER:*firefox" -o output-C.xml -l log-C.xml -r report-C.html path/to/tests/c
```

The same issue as above applies: make sure to specify different output, log and report files, otherwise logs will be unusable. Rebot can be used to merge the results. All `pybot` instances can, of course, be started in parallel.

# Run Tests from a Single Suite in Parallel #

If you're fine with the choices listed above and just willing to play around with GRID first, stop reading. This section digs a little deeper into test orchestration and presents a was on how to execute all tests in a single suite in parallel.
Since it is not easy to make sure that test 17 from suite A does not interferes with test 47 from suite B if by chance they are executed at the same time, it is a good idea to make a script that only executes tests from one suite but executes them using multiple `pybot` instances. This way you only need to make sure that all the tests in _one_ suite do not have a potential to interfere with each other. The basic idea is that every test that can be executed in parallel is tagged with "parallel". The script scans for those tests and splits them up into multiple `pybot` calls. These calls will be executed in parallel. Once they are done, all tests that are not tagged as "parallel" will be executed one-by-one. At the end results will be merged into a single log file.

The code to do this is found below, without any guarantee that it will work for you. To use the script, invoke `parabot.bat` instead of `pybot` with the test suite as argument.

`parabot.py` -- main test execution class
```
# -*- coding: utf-8 -*-
#
# Script to execute test cases from one suite in parallel
# by thomas klein / 2009
#

# imports
from robot.running import TestSuite
from robot import utils
from robot.conf import settings
import os, glob
import subprocess
import time
from datetime import datetime
import sys
import getopt
import ParabotConfig as config

# save current time to calculate execution time at the end of the script
startTime = datetime.now()

# global vars
suite_name = "No suite defined yet" # specified via args
includeTags = [] # specified via args
excludeTags = [] # specified via args
para_tag = "parallel"
clientCwd = "No cwd defined" # specified via testsuite from args
forceSerialExecution = False
baseDir = "./"


# reading variables from ParabotConfig
max_parallel_tests = config.MAX_PARALLEL_TESTS
min_test_per_block = config.MIN_TESTS_PER_BLOCK
logFolder = config.LOG_DIR
antBatch = os.path.abspath(config.ANT_BATCH_FILE)
seCwd = os.path.abspath(config.SELENIUM_GRID_DIR)
startSelenium = config.AUTOSTART_SELENIUM
browser = config.SELENIUM_BROWSER


# Methods #####################################################################################################

def splitTestsToBlocks(tests):
    """ Splits a list of tests into several small lists (blocks) and returns a list containing these lists.
    'MAX_PARALLEL_TESTS' and 'MIN_TESTS_PER_BLOCK' will be used as criteria for splitting the list. For 
    details see configuration hints in ParabotConfig.py.
    """
    para_test_blocks = []
    number_of_blocks = -1
    if len(tests) / min_test_per_block > max_parallel_tests:
        number_of_blocks = max_parallel_tests
    else:
        number_of_blocks = len(para_tests) / min_test_per_block
    for i in range(0, number_of_blocks):
        para_test_blocks.append([])
    current_block = 0
    for test in tests:
        block = current_block%number_of_blocks
        para_test_blocks[block].append(test)
        current_block = current_block+1
    return para_test_blocks

def startSeleniumHub():
    """ Starts a Selenium Hub on localhost:4444 and return the process handle    
    """
    hubScript = "%s launch-hub" % antBatch
    hubLog = open(os.path.join(logFolder,"Parabot_Hub_Log.txt"), "w")
    print "Starting Selenium Hub ..."
    process = subprocess.Popen(hubScript, cwd=seCwd, stdout=hubLog, stderr=hubLog)
    time.sleep(10)
    return process

def startSeleniumRC(port):
    """ Starts a Selenium Remote Control connecting to a Selenium hub on localhost:4444. Process handle to
    the RC will be returned.
    'port' is the port the RC will be using to communicate with the hub
    """
    rcScript = "%s -Dport=%s -Dhost=127.0.0.1 -DhubURL=http://127.0.0.1:4444 -Denvironment=\"%s\"" \
               " launch-remote-control" % (antBatch, port, browser)
    rcLog = open(os.path.join(logFolder,("Parabot_RC_%s_Log.txt" % port)), "w")
    print "Starting Selenium RC (%s) on port %s ..." % (browser,port)
    process = subprocess.Popen(rcScript, cwd=seCwd, stdout=rcLog, stderr=rcLog)
    return process

def startSeleniumRCs(howMuch):
    """ Starts a given number of Selenium Remote Controls (calls startSeleniumRC(port)) and returns a list 
    of processes referring to the RCs. Ports 5556 and up will be used for the RCs.
    'howMuch' defines the number of RCs to start
    """
    rcs = []
    for i in range(5556, 5556+howMuch):
        rcs.append(startSeleniumRC(i))
    time.sleep(5)
    return rcs

def startPybot(name, tests, suite, args=[]):
    """ Creates a pybot object, starts it and returns the object
    'name' is the name for the pybot (will be used for log outputs)
    'tests' is a list of tests to be executed by the pybot
    'suite' is the filename of the test suite containing the 'tests'
    'args' (optional) is a list of additional parameters passed to pybot
    """
    pybot = Pybot(name)
    pybot.start(tests, suite, args)
    return pybot

def generateReportAndLog(xmlFiles, reportFile, logFile):
    """ Calls RobotFrameworks rebot tool to generate Report and Log files from output.xml files
    'xmlFiles' is a list of output.xml files from jybot / pybot
    'reportFile' is the path+name of the report.html file to be written
    'logFile' is the path+name of the log.html file to be written
    the global variable 'suite_name' will be used a report title
    """
    rebotCommand = "rebot.bat --log %s --report %s --reporttitle \"%s\" " % (logFile, reportFile, suite_name)
    for file in xmlFiles:
        rebotCommand = rebotCommand + "%s " % file
    rc = os.system(rebotCommand)
    return rc

def parseArgs(argv):
    """ Parses command line arguments like the testsuite name and additonal parameters 
    Expects the command line args without the python class as parameter argv (sys.argv[1:])
    Fails and aborts script if args don't match the expected format
    """
    global includeTags, excludeTags, suite_name, clientCwd, forceSerialExecution, baseDir, logFolder
    if len(argv)<1:
        usage()
        sys.exit(2)
    try:
        # checking for additional options (-h -i -e etc)
        opts, args = getopt.getopt(argv, "hi:e:fb:", ["help", "include=", "exclude=", "forceserial", "basedir="])
        for opt, arg in opts:
            if opt in ("-h", "--help"):
                usage()
                sys.exit(2)
            elif opt in ("-i", "--include"):
                includeTags.append(arg)
            elif opt in ("-e", "--exclude"):
                excludeTags.append(arg)
            elif opt in ("-f", "--forceserial"):
                forceSerialExecution = True
                print "Forcing serial test execution!"
            elif opt in ("-b", "--basedir"):
                baseDir = arg
                if len(argv)==2:
                    usage()
                    sys.exit(2)
        if len(includeTags) > 0:
            print "Including Tags: %s" % includeTags
        if len(excludeTags) >0:
            print "Excluding Tags: %s" % excludeTags
    except getopt.GetoptError:
        print "Error while parsing command line arguments"
        sys.exit(2)
    # last argument is test suite name
    suite_name = argv[len(argv)-1]
    clientCwd, suite_name = os.path.split(suite_name)
    if len(clientCwd) == 0:
        clientCwd = "./"
    suite_name = os.path.join(baseDir, suite_name)
    logFolder = os.path.join(clientCwd, logFolder)
    logFolder = os.path.abspath(logFolder)
    print "Working dir: %s" % os.path.realpath(clientCwd)
    print "Base dir: %s" % os.path.realpath(baseDir);
    print "Log dir: %s" % logFolder
    print "Executing suite: %s" % suite_name

def getDynArgs(index):
    """ Reads the DYN_ARGS variable from the config file and parses it into a list of argument strings
    like --variable name:"value".
    This list can be passed to the Pybot start() method as args[] list.
    """
    arglist = []
    for row in config.DYN_ARGS:
        valueIndex = index
        if len(row) < 2:
            print "Error reading DYN_ARGS: Row is invalid: %s. Row will be skipped!" % row
        else:
            varName = row[0]
            values = []
            i = 1
            while i < len(row):
                values.append(row[i])
                i = i+1
            if valueIndex >= len(values):
                valueIndex = (len(values)-1) % valueIndex
            varValue = values[valueIndex]
            arglist.append("--variable %s:\"%s\"" % (varName, varValue))
    return arglist

def usage():
    """ Prints usage information for Parabot """
    print ""
    print "Usage: python parabot.py [options] <testsuite.tsv>"
    print ""
    print "<testsuite.tsv> can be absolute or relative path + filename of a testsuite."
    print "The containing folder will be used as working directory"
    print ""
    print "Options:"
    print "-h\t--help\t\tThis screen"
    print "-i\t--include\tInclude a tag"
    print "-e\t--exclude\tExclude a tag"
    print "-f\t--forceserial\tForces serial test execution"
    print "-b\t--basedir\tSet parabots base dir"
    print ""

# helper classes ##############################################################################################

class Pybot():
    """ Helper class to interact with RobotFrameworks pybot script to execute tests / test suites.    
    """
    name = ""
    tests = []
    suite = ""
    args = []
    output = ""
    process = -1
    running = False
    
    def __init__(self, name):
        """ Constructor, creates the object and assigns the given 'name'.
        """
        self.name = name
        print "Created pybot %s." %name
    
    def start(self, tests, suite, args=[]):
        """ Starts the pybot script from RobotFramework executing the defined 'tests' from the given 'suite'.
        'tests' is a list of tests to be executed by the pybot
        'suite' is the filename of the test suite containing the 'tests'
        'args' (optional) is a list of additional parameters passed to pybot
        """
        self.tests = tests
        self.suite = suite
        self.args = args
        temp, suiteName = os.path.split(suite_name)
        self.output = "%s_%s_Output.xml" % (suiteName, self.name)
        pybotCommand = "pybot.bat "
        for test in self.tests:
            pybotCommand = pybotCommand + "-t \"%s\" " % test
        for arg in self.args:
            pybotCommand = pybotCommand + arg + " "
        pybotCommand = pybotCommand + "-o %s " % os.path.join(logFolder, self.output)
        pybotCommand = pybotCommand + "-l NONE "
        pybotCommand = pybotCommand + "-r NONE "
        pybotCommand = pybotCommand + "-N \"%s %s\" " % (suiteName, self.name)
        pybotCommand = pybotCommand + suite
        #print pybotCommand
        pyLog = open(os.path.join(logFolder, ("Pybot_%s_Log.txt" % self.name)), "w")
        print "Starting pybot %s ..." % self.name
        self.running = True
        self.process = subprocess.Popen(pybotCommand, cwd=clientCwd, stdout=pyLog, stderr=pyLog)
    
    def isRunning(self):
        """ Polls the pybot subprocess to check if it's running. Will return true if the process is running.
        Returns false if the process hasn't been started or has finished already.
        """
        if not self.running:
            return False
        elif self.process.poll() == 0 or self.process.returncode >= 0:
            return False
        else:
            return True
    
    def stop(self):
        """ Kills the pybot subprocess.
        """
        os.system("taskkill /T /F /PID %s" % self.process.pid)
        self.running = False

# MAIN SCRIPT #################################################################################################

# parsing command line arguments
parseArgs(sys.argv[1:])

# generating two lists containing parallel and serial tests
para_tests = []
seri_tests = []
try:
    # RobotFramework 2.0.4
    suite = TestSuite(os.path.join(clientCwd, suite_name), process_curdir=False)
except Exception:
    # RobotFramework 2.5
    suiteOps = settings.RobotSettings()
    suite = TestSuite([os.path.join(clientCwd, suite_name)], suiteOps)

for test in suite.tests:
    # special treatment for tests without tags:
    # include them into serial execution as long as no include tags are defined
    if not test.tags and len(includeTags)==0:
        seri_tests.append(test.name)
    # tests with tags:
    # filter excluded tests (if any), then filter included tests (if any), then scan for
    # parallel keyword and assign to parallel / serial block
    elif len(excludeTags)==0 or not test._contains_any_tag(excludeTags):
        if len(includeTags)==0 or test._contains_any_tag(includeTags):
            if test._contains_tag(para_tag) and not forceSerialExecution:
                para_tests.append(test.name)
            else:
                seri_tests.append(test.name)

# output serial test list
print ""
print "Serial tests:"
if len(seri_tests) == 0:
    print "NONE"
else:
    for test in seri_tests:
        print test
    
# splitting parallel tests into blocks 
para_test_blocks = splitTestsToBlocks(para_tests)

# output parallel test list
print ""
print "Parallel Blocks:"
for block in para_test_blocks:
    print ""
    for test in block:
        print test
if len(para_test_blocks) == 0:
    print "NONE"
print ""


# starting selenium components
if startSelenium:
    seHub = startSeleniumHub()
    numberOfRCs = max(len(para_test_blocks), 1)
    seRCs = startSeleniumRCs(numberOfRCs)

# starting parallel pybots
i = 0;
pybots = []
for block in para_test_blocks:
    dynArgs = getDynArgs(i);
    pybots.append(startPybot("paraBlock_%s" % i, block, suite_name, dynArgs))
    i = i+1
    # delay start of next pybot
    time.sleep(5)

# waiting for parallel tests to finish
finished = False
while not finished:
    time.sleep(10)
    message = "Finished: %s" % finished
    finished = True
    for pybot in pybots:
        message = "%s | %s: " % (message, pybot.name)
        if pybot.isRunning():
            finished = False
            message = "%s%s" % (message, "Running")
        else:
            message = "%s%s" % (message, "DONE")
    print message
        
print "Parallel Tests finished ..."


# running serial block
pybot = None
if len(seri_tests) > 0:
    print ""
    print "Starting serial tests ..."
    pybot = startPybot("serial_block", seri_tests, suite_name, getDynArgs(0))
    while pybot.isRunning():
        time.sleep(5)
        
    print "Serial tests finished"
    print ""


# killing Selenium Hub / RCs
if startSelenium:
    print "Killing Selenium Hub and RCs"
    os.system("taskkill /T /F /PID %s" % seHub.pid)
    for rc in seRCs:
        os.system("taskkill /T /F /PID %s" % rc.pid)
    print ""


# merging outputs to one report and log
print "Generating report and log"
temp, suiteName = os.path.split(suite_name)
report = "%s_Report.html" % os.path.join(logFolder, suiteName)
log = "%s_Log.html" % os.path.join(logFolder, suiteName)
outputXmls = []
if pybot != None:
    outputXmls.append(os.path.join(logFolder, pybot.output))
for pybot in pybots:
    outputXmls.append(os.path.join(logFolder, pybot.output))

reportRC = generateReportAndLog(outputXmls, report, log)


# delete XML output files after generating the report / log (if report generation 
# returned zero)
#if reportRC == 0:
#    for outXML in outputXmls:
#        os.remove(outXML)

# calculating test execution time
endTime = datetime.now()
executionTime = endTime - startTime
print ""
print "Execution time: %s" % executionTime
```

`ParabotConfig.py` -- config file for `parabot`:
```
###############################################################################################################
# Configure Selenium GRID:
# Parabot is able to auto-start Selenium Hub and Remote Controls, to enable this feature set 
# AUTOSTART_SELENIUM to True. To disable it set the variable to False. If the feature is enable
# ANT_BATCH_FILE and SELENIUM_GRID_DIR need to be specified.
# Note: if the feature is disabled Parabot assumes a Selenium Hub with sufficient Remote Controls
# is running on http://127.0.0.1:4444. One RC per test block (see below) will be required.
AUTOSTART_SELENIUM = True
# Absolute reference to Apache ANTs "ant.bat" file
ANT_BATCH_FILE = "..\\Ant\\bin\\ant.bat"
# Absolute reference to the Selenium-GRID directory in a RobotTest package
SELENIUM_GRID_DIR = "..\\Selenium"
# Browser environment RCs will be providing, e.g. *chrome or *firefox (needs to match with the browser 
# your tests will be requesting)
SELENIUM_BROWSER = "*firefox"
###############################################################################################################
# Configure Logging:
# A directory to place log files in
LOG_DIR = "..\\Logs"
###############################################################################################################
# Configure parallelization:
# Test suite will be split into blocks of x tests, these blocks will be executed in parallel.
# MAX_PARALLEL_TESTS defines the maximum number of blocks and therefore the maximum number of 
# tests being executed in parallel. To avoid blocks from containing to few tests, MIN_TESTS_PER_BLOCK
# specifies the minimum number of tests required to build a block.
# E.g. a suite with 20 parallel Tests will be split into: 
# - 5 Blocks with MAX_PARALLEL_TESTS=5 and MIN_TESTS_PER_BLOCK=3
# - 2 Blocks with MAX_PARALLEL_TESTS=5 and MIN_TESTS_PER_BLOCK=10
MAX_PARALLEL_TESTS = 5
MIN_TESTS_PER_BLOCK = 1
###############################################################################################################
# Dynamic pybot variables:
# Specifies an 3D-array with variables passed to the single pybot instances
# Each row contains a variablename - value(s) combination (array, name at index 0, values at 1++)
# One variable value will be passed to each python instance using --variable name:value
# If multiple values are defined parabot will iterate over the values and assign one to each pybot
DYN_ARGS =  [
    # specify different users
    ["USER", "Hans", "Klaus", "Peter", "Martin", "Eric"],
    # passwords
    ["PASS", "HansPassword", "KlausPassword", "PetersPassword", "MartinsPassword", "EricsPassword"]
]
```

`parabot.bat` -- start-up script for `parabot` (you probably need to modify this to your needs)
```
@echo off

set thisDir=%~dp0
set oldDir=%CD%
set python=%thisDir%..\Python\python.exe
set PYTHONPATH_BAK=%PYTHONPATH%
set PYTHONPATH=%PYTHONPATH%;%thisDir%..\Tests\CommonLibs
set PATH_BAK=%PATH%
set PATH=%PATH%;%thisDir%..\Python

cd %thisDir%
%python% Parabot.py -b %oldDir%\ %*
cd %oldDir%

set PYTHONPATH=%PYTHONPATH_BAK%
set PYTHONPATH_BAK=
set python=
set oldDir=
set PATH=%PATH_BAK%
set PATH_BAK=
```