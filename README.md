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

### sitemapcrawler.jmx

This plan will simulate users that visit random URLs taken from a sitemap file.
The first request it will do is fetch the sitemap, then it will visit the homepage,
and then it will visit some random URLs taken from the sitemap.

The following variables are available:

variable | description
--- | ---
SERVER | IP address of the server to test
CONCURRENCY | Maximum number of concurrent users to test
DURATION | Duration of the test in seconds
SITEMAP_URL | URL path to the Google sitemap
NUM_PAGES | Number of pages a user will visit before being replaced by another user

The test will start with one user and incrementally use more users until $CONCURRENCY
during the given $DURATION. Each user will apart from the homepage visit $NUM_PAGES with a
speed of about 3 pages per second.

## Running headless

```
jmeter -n -p user.properties -t <testplan.jmx> -l <outputfile.jtl> -Jserver=<ip address>
```

