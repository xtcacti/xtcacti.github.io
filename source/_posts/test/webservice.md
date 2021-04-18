---
title: webservice
date: 2021-04-15 23:25:05
tags: webservice
---

## Web Service
### what
1. service available over web
2. enables communication between application over the web
3. provides a standard protocol/format for communication
4. platform indenpendent communition
5. using web services two different applications can talk to each other and exchange data/information

### how
- Server (Service Provider)
  - a web service provider develops/implements the application(web service) and make it available over the internet(web) 
- Client (Service Consumer)
- Client ----REQUEST----> Server
- Client <---RESPONSE---- Server
- Menium:HTTP/INTERNET
- FORMAT:XML/JSON
- two web service implements:
  1. SOAP (Simple Object Access Protocol)
    - Medium:HTTP(POST)
    - Format:XML
  2. REST (RE:presentational State Transfer)
    - Menium:HTTP(POST,GET,PUT,DELETE...)
    - Format:XML/JSON/TEXT/YAML...

## WSDL & UDDI
Consumer need to know:
- what are the services available？
- what are the request and response parameters?
- how to call the web service?

Service Provider publishes an interface for his web services that describes all arrtibutes o fthe web serives

This is XML based interface and is called - WSDL
- WSDL: Web Services Description Language

A web service provider publishes his web service through wsdl on an online directory from where consumers can query and search the web services. This online directory/registry is called UDDI
- UDDI: Universal Description,Discovery and Integration
- is an XML based standard for publishing and finding web services

## SOAP Web Services
A web service that compiles to the soap web services specifications is a soap web services
1. who defines and dictates these standards?
- W3C (World Wide Web Consortium)
2. what are these specifications/standards?
- Basic
  - SOAP
  - WADL
  - UDDI
- Extended
  - WS - Security
  - WS - Policy
  - ...
- SOAP: Simple Object Access Protocol
  - All information/message exchange happens over a common format:XML
  - XML messges have a defined structure:SOAP MESSAGE
  - SOAP MESSAGE consist of:Envelop (Header Body)

## Rest Web Services
### what is REST
- REpresentational State Transfer

A Resource's Representation is transferred between server and client

a web servie that communications/exchanges information between 2 applications using REST architecture/principles is called a Restful Web Service

### what are the principles/constrains od REST architecture?
1. Uniform Interface
   1. Resource: everything is a resource
   2. URI: any resource/data can be accessed by a URI
   3. HTTP: make explicit use of HTTP methods
- Using HTTP Methods along with URI, we can access/modify any resource or resource information

   |Request|Response|
   |----|----|
   |Get http://example.com/employees |list of employees|
   |Get http://example.com/employees/10 |detail of employee with id=10|
   |Post http://example.com/employees +Data of new employee|id of new employee|
   |Delete http://example.com/employees/10 |deletes employee with id=10|
   |Put http://example.com/employees/10 +Data to be changed|modifies data for emplyee 10|
2. Stateless
   - all client-server communitions are stateless 
   - improves Web Service Performance
3. Cacheable
   - happens at client side
4. Layered System
   - multiple layers can exist between client and server,e.g. Proxies Gateways
   - improves performance and scalability
5. Code On Demand(Optional)
   - ability to download and execute code on client side

## Authorization 授权 & Authentication 认证
- Auhthorizatin: what can you do or what access do you have?
- Authentication: who you are?
- Why do we have Authorization and NOT Authentication in API Request?

## How to create API documentation through WSDL url?
## How to compare two wsdl?