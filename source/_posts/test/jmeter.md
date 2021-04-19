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

## How to use Blazemeter to Record JMeter Tests
1. create Blazemeter account
2. get blazemeter extension
3. login to Blazemeter
4. record test
5. save JMX
6. Add JMX in JMeter and Run

## How to get data from csv file
1. Add - Config Element - CSV Data Set Config
2. create csv file and add data
3. refer csv file in JMeter's csv data set config
4. refer values from csv file using syntax ${variableName}

## JMeter Config Elements - for HTTP (Web Test Plan)
- Elements that are executed before the sampler requests at the same level
- Configuration elements can be used to set up defaults and variables for later use by samplers. Note that these elements are processed at the start of the scope in which they are found, i.e. before any samplers in the same scope
- Demo app - https://opensource-demo.orangehrmlive.com/

## How to run JMeter from command line
- GUI consumes memoryy,slower
- integrate with any external process CI CD
1. How to run JMeter from command line?
2. How to log results?
- goto jemeterbin folder
- windows: `jmeter -n -t "location of your test" -l "location of your result"`
- mac/linux: `sh jmeter -n -t "location of your test" -l "location of your result"`
3. How ti see command line help and options?
- `jmeter -h`
- `jemter.bat -?`
4. How to run fomr any location on your system?
- add in Path env variables

## Hor to create HTML Reports from command line & GUI
1. How to create html dashboard reports from command line
2. How to create html dashboard reports from standard csv result file
3. Study the html dashboard reports
- create a test plan or use existing test plan
- open command line goto jmeter bin folder  
- generate report from run test plan `jmeter -n -t "C:\Workspace\learn-automation\6-Jmeter\Test Plan - html report.jmx" -l "C:\Workspace\learn-automation\6-Jmeter\result-log.csv" -e -o "C:\Workspace\learn-automation\6-Jmeter\Reports"`
- generate report from csv result `jmeter -g "C:\Workspace\learn-automation\6-Jmeter\result-log.csv" -o "C:\Workspace\learn-automation\6-Jmeter\Reports"`
4. How to generate from GUI?
- Tools - Generate html report

## How to extend JMeter | JMeter plugins manager
Plugins - https://jmeter-plugins.org/
1. find plugins
- download plugins manager jar form https://jmeter-plugins.org/wiki/PluginsManager/
2. install
- add jat to jmeter/lib/ext
- restart jmeter
- Options - JMeter Plugins Manager
3. uninstal
4. upgrade

## How to create TEST API Request in JMter
- GET,POST,PUT,DELETE
- HTTP Request
- REST demo:https://reqres.in/

## How to create a SOAP API Request
1. How to add Request Sampler
2. How to add Headers
3. How to add Authorsation
4. How to add Body
5. How to add Assertions
6. How to run and check results
- SOAP demo:http://www.dneonline.com/calculator.asmx?WSDL
- HTTP Request
  - Body(XML)
  - Header(Content-Type, SOAPACTION)
- Response Assertion
- Assertion Result

## Functions & Veriables
1. What are functions?
- methods used to populate fields in any other element of a test plan
- Syntax:
  - `${__funcName}`
  - `${__funcName(var1,var2,...)}`
2. What are variables?
- contains that can store values which can be referred in any element within a thread
- Syntax:
  - `${varName}`
3. How to use functions and variables?


