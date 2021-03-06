# Load and performance testing using Apache JMeter

Follow these steps to perform a load test:

## Setup

1. Install jmeterfrom http://jmeter.apache.org or `apt-get install jmeter`.
2. Install the standard set of jmeter plugins from
   http://jmeter-plugins.org, by downloading the zip file and extracting
   it to the jmeter directory. If you installed the debian/ubuntu package,
   this directory is `/usr/share/jmeter`.


## Running tests

Open jmeter and open a test plan. The Test Plan node in the tree contains 
configuration variables that can be set to control testing.

## Server metrics

The plans can connect to the server to monitor resource usage. This will require
an agent to be running on the server.

Unfortunately the composite graph has a reference to the server name in the PerfMon graphs,
so for each different server you test you'll have to replace the PerfMon graphs in on the
Graphs tab.

### sitecrawler.jmx

This plan will simulate users that click random URLs, starting from the homepage
of a site.

variable | description
--- | ---
SERVER | IP address of the server to test
CONCURRENCY | Maximum number of concurrent users to test
DURATION | Duration of the test in seconds
NUM_PAGES | Number of pages a user will visit before being replaced by another user


![This is where the settings live](https://raw.githubusercontent.com/ByteInternet/hypernode-performance-test/master/media/jmeter-crawler-settings.png)


## Running headless

```
jmeter -n -p user.properties -t <testplan.jmx> -l <outputfile.jtl> -Jserver=<ip address>
```

