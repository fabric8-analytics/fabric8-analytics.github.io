# e2e test plan to match with SLO

This is a plan to improve the existing e2e tests to better match with defined SLOs.
At the end I also mention REST API performance tests that are related to e2e tests.



## SLOs

### Success rate of LSP calls (to flag CVEs) to analytics service

#### Indicators

* 95%

#### Proposed test changes

1. Retrieve statistic with most used combinations of ecosystem+package+version
1. Implement new tests to call REST API with manifest to check and test results
1. Expected results = 100% accuracy for e2e tests



### Latency for LSP calls (to flag CVEs) to analytics service 

#### Indicators

* two seconds per each LSP call

#### Proposed test changes

1. Implement new test steps to track time (start time + end time)
1. Implement new test steps to check the duration between start time and end time
1. Use tests from previous point and add check for duration
1. Expected results to be checked by new tests <= 2 seconds per analysis



### Success rate of dependency stack analysis report generation

#### Indicators

* Upto 50 dependencies (direct + transitive):   99%
* Upto 100 dependencies (direct + transitive):  95%
* Above 100 dependencies (direct + transitive): 90%

#### Proposed test changes

1. Prepare manifest files with 50 direct dependencies for each ecosystem
1. Implement tests (one for each ecosystem) to check those dependencies
1. Prepare manifest files with 10 direct + 40 transitive dependencies for each ecosystem
1. Implement tests (one for each ecosystem) to check those dependencies
1. Prepare manifest files with 100 direct dependencies for each ecosystem
1. Implement tests (one for each ecosystem) to check those dependencies
1. Prepare manifest files with 10 direct + 90 transitive dependencies for each ecosystem
1. Implement tests (one for each ecosystem) to check those dependencies
1. Prepare manifest files with 150 direct dependencies for each ecosystem
1. Implement tests (one for each ecosystem) to check those dependencies
1. Prepare manifest files with 20 direct + 100 transitive dependencies for each ecosystem
1. Implement tests (one for each ecosystem) to check those dependencies



### Latency of stack analysis for applications

#### Indicators

* Upto 50 dependencies (direct + transitive): 60 seconds
* Upto 100 dependencies (direct + transitive): 90 seconds
* Above 100 dependencies (direct + transitive): 180 seconds

#### Proposed test changes

1. We will use the same tests as described in previous point
1. Additional check for 60 seconds duration will be used in first set
1. Additional check for 90 seconds duration will be used in first set
1. Additional check for 180 seconds duration will be used in first set



### Availability of analytics service (online and offline backend services)

#### Indicators

* 97%

#### Proposed test changes

1. Nothing to do with e2e, needs to be monitored on Prometheus



### [Concurrency] # of concurrent Analytics API calls being served 

#### Indicators

* % of successful API calls if < 300 concurrent total API calls: 99%
* % of successful API calls if( > 300 and < 1000) concurrent total API calls: 95%
* % of successful API calls if( > 1000 and < 2000) concurrent total API calls: 90%

#### Proposed test changes

1. Nothing to do with e2e tests, this metrics are related with performance tests (already implemented)



## Other improvements

There are other improvements planned in e2e tests, especially:

### Stack analysis

1. Prepare additional checks for stack analysis results (need to have proper documentation with explanation of all attributes)
1. Prepare stacks with unknown dependencies (currently it is used only in reproducers)

### Component analysis

1. Retrieve list of components with known CVEs
1. Prepare new tests to check CVEs (values, score, ...) for prepared list of components



# Releated tests

1. Update a2t (REST API performance tests) to check the stack analysis results
1. Run a2t regularly with heavy load on stage
1. Run a2t regularly with small load on production

