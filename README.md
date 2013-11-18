TestLink API Python Client
==========================

Copyright 2011-2013 
James Stock, Olivier Renault, Luiko Czub, TestLink-API-Python-client developers

License [Apache License 2.0]

Introduction
------------

TestLink-API-Python-client is a Python XMLRPC client for the [TestLink API].

Initially based on the James Stock testlink-api-python-client R7 and  Olivier 
Renault [JinFeng] idea - an interaction of [TestLink], [Robot Framework] and [Jenkins].

TestLink-API-Python-client delivers two main classes
*   TestlinkAPIGeneric - Implements the Testlink API methods as generic PY 
    methods with error handling.
    *   Allows the configuration of arguments for these API method as positional
        or optional arguments.
    
*   TestlinkAPIClient - Inherits Testlink API methods from the generic client
    TestlinkAPIGeneric and defines service methods like "countProjects".
    *   Change the configuration for positional and optional arguments in a way, 
        that often used arguments are positional (consistent with v0.4.0).

Directory Layout
----------------

src/
*   Source for TestLink API Python Client

tests/
*   Unit Tests for TestLink API Python Client

examples/
*   Examples, how to use the TestLink API Python Client

Installation
------------

### TestLink configuration
The testLink configuration (config.inc.php or custom_config.inc.php) must have enabled the api interface
*   $tlCfg->api->enabled = TRUE;
   
The user specific devKey are created inside TestLink, see
*   My Settings -> API interface - Personal API access key [Generate a new key]

### Install TestLinkAPI into a virtualenv environment

```
[PYTHON27]\Scripts\virtualenv [PYENV]\testlink
[PYENV]\testlink\Scripts\activate
pip install TestLink-0.4.5.zip
```

Usage
-----

### Connect TestLink in a python shell

```
[PYENV]\testlink\Scripts\activate
set TESTLINK_API_PYTHON_SERVER_URL=http://[YOURSERVER]/testlink/lib/api/xmlrpc/v1/xmlrpc.php
set TESTLINK_API_PYTHON_DEVKEY=[Users devKey generated by TestLink]
python
>>> import testlink
>>> tls = testlink.TestLinkHelper().connect(testlink.TestlinkAPIClient)
>>> tls.countProjects()
3
>>> tls.getTestCase(None, testcaseexternalid='NPROAPI3-1')
[{'full_tc_external_id': 'NPROAPI3-1', 'node_order': '0', 'is_open': '1', 'id': '2757', ...}] 
```

### Run example with command line arguments

```
[PYENV]\testlink\Scripts\activate
python example\TestLinkExample.py 
               --server_url http://[YOURSERVER]/testlink/lib/api/xmlrpc.php
               --devKey [Users devKey generated by TestLink]
```
```
[PYENV]\testlink\Scripts\activate
set TESTLINK_API_PYTHON_SERVER_URL=http://[YOURSERVER]/testlink/lib/api/xmlrpc/v1/xmlrpc.php
set TESTLINK_API_PYTHON_DEVKEY=[Users devKey generated by TestLink]
python example\TestLinkExampleGenericApi.py
```

### Run unittests with TestLink Server interaction

```
[PYENV]\testlink\Scripts\activate
set TESTLINK_API_PYTHON_SERVER_URL=http://[YOURSERVER]/testlink/lib/api/xmlrpc.php
set TESTLINK_API_PYTHON_DEVKEY=[Users devKey generated by TestLink]
cd test\utest
python -m unittest testlinkapicallservertest testlinkapi_online_test
```

### Run unittests without TestLink Server interaction

```
[PYENV]\testlink\Scripts\activate
cd test\utest
python -m unittest testlinkhelpertest testlinkapi_offline_test
```

### Changes with TestLink 1.9.7

The SERVER_URL path has changed with TestLink 1.9.7.
Use http://[YOURSERVER]/testlink/lib/api/xmlrpc/v1/xmlrpc.php

Download
--------

latest stable release see [SourceForge]
*    please read [v0.4.5 release notes](https://github.com/lczub/TestLink-API-Python-client/releases/tag/v0.4.5)
     for changes between v0.4.0 and v0.4.5    

development version see [Releases]

Help
----

Questions, Enhancements, Issues are welcome under [Issues]

For (nearly all) implemented API methods you find in 
[example/TestLinkExample.py](example/TestLinkExample.py) 
an example, which although prints the reponse.

The Teslink API Client can be asked, what arguments a API method expects

```
import testlink
tlh = testlink.TestLinkHelper()
tls = tlh.connect(testlink.TestlinkAPIClient)
print tls.whatArgs('createTestPlan')
createTestPlan(<testplanname>, <testprojectname>, [note=<note>], [active=<active>], [public=<public>], [devKey=<devKey>])
 create a test plan 
```

or a description of all implemented API method can be generated

```
import testlink
tlh = testlink.TestLinkHelper()
tls = tlh.connect(testlink.TestlinkAPIClient)
for m in testlink.testlinkargs._apiMethodsArgs.keys():
	print tls.whatArgs(m), '\n'
```

TestLink-API-Python-client developers
-------------------------------------
*   [James Stock], [Olivier Renault], [lczub]
*   [g4l4drim], [pade], [anton-matosov], [citizen-stig]
*   anyone forgotten?


[Apache License 2.0]: http://www.apache.org/licenses/LICENSE-2.0
[JinFeng]: http://www.sqaopen.net/blog/en/?p=63
[TestLink API]: http://www.teamst.org/_tldoc/1.8/phpdoc_api/TestlinkAPI/TestlinkXMLRPCServer.html
[TestLink]: http://testlink.org/
[Robot Framework]: http://code.google.com/p/robotframework
[Jenkins]: http://jenkins-ci.org/
[Releases]: https://github.com/lczub/TestLink-API-Python-client/releases
[SourceForge]: http://sourceforge.net/projects/testlink-api-python-client/files/latest/download
[Issues]: https://github.com/lczub/TestLink-API-Python-client/issues
[Olivier Renault]: https://github.com/orenault/TestLink-API-Python-client
[pade]: https://github.com/pade/TestLink-API-Python-client
[g4l4drim]: https://github.com/g4l4drim/TestLink-API-Python-client
[James Stock]: https://code.google.com/p/testlink-api-python-client/
[lczub]: https://github.com/lczub/TestLink-API-Python-client
[anton-matosov]: https://github.com/anton-matosov/TestLink-API-Python-client
[citizen-stig]: https://github.com/citizen-stig/TestLink-API-Python-client
