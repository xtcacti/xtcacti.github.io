---
title: jmeter
date: 2021-04-17 18:10:37
tags: jmeter
---


## what is Jmeter
- Performance test application
- Build using java
- Free & Open Source
- Recording
- CLI
- Reports

## install Jmeter
1. check java is installed on your system
- `java -version` on cmd
2. download Jmeter and unzip
3. start Jmeter
- Windows -> jmeter/bin -> jmeter.bat
- Mac -> open terminal -> jmeter/bin -> sh jmeter.sh

## create first Jmeter test
1. Start Jmeter
2. Create a TestPlan
3. Create a Thread Group(Users)
4. Add a Sampler(Http)
5. Add Listeners
6. Run the Test

## Jmeter Listeners(Reporting)
- used for reporting
- listener = elements that gather information about the performance test used to view results/metrics of the test
- 1000 ms = 1 sec
1. View Results in Table
- Latency: start get response - finished response
2. View Result Tree
3. Aggregate Report
4. Graph Results
5. Summary Report
6. Simple Data Writer

## Assertions
- Assertions = check on the Request/Response
1. Response Assertion
2. Duration Assertion
3. Size Assertion
4. HTML Assertion
5. XML JSON Assertion
6. XPATH Assertion

## Jmeter HTTP(s) Test Script Recorder
- what
- why
- when
- how
1. how to record your test on Jmeter?
2. how to add & use Test Script Recorder?
3. how to add & use Recording Controller?
4. how to use proxy on Firefox,Chrome and System?
5. how to add SSL Certificate?
6. how to do Request Filter?
7. how to use Recording Template?