---
title: postman
date: 2021-04-16 15:05:31
tags: test
---

## what
- API Client
- develop,test.share,document APIs

## COLLECTION
### what
- collection is a group of api requests that can be stroed and saaved in logical arrangement
- forms the basis for advanced operations in POSTMAN
### how
1. run?
2. analyse?

## Veriables
1. what
- element(data srouce) that can take different values

2. why
- to reuse values at multiple places avoid repetition
- ot avoid re-work when value changes

3. how to set and get veriables through scripting 
- get: `pm.variables.get("url");`
- set: `pm.variables.set("name","xtcacti");`

## Environment
Env is a set of key-value pairs

## Script Snippets
1. how to create quick scripts using Snippets

## First Test
1. what are test in postman?
- postman tests are javascript code that is executed after receiving the response
2. create tests at REQUEST level~
3. create tests at FOLDER level~
4. create tests at COLLECTION level~

## DEBUG
1. debug
2. open console
3. clear logs
4. `console.log()/info()/warn()/error()`
5. Develop - DevTools

## run from Command Line
1. install node.js
2. install newman
3. export collection and run from commandline
- newman is a command line collection runner for Postman
- `newman run exportname.json`
- `newman run -h`

## run form Jenkins
1. how to setup postman on Jenkins?
2. hor to run postman on Jenkins?

## WORKSPACES
1. what is workspaces?
- an area where you can group, organize and manage collections
2. create & manage workspaces
3. share collections in workspaces
4. remove collection form workspaces

## DDT - Data Driven Testing
How to use csv and json data files
1. how to get data from csv file?
2. how to get data from json file?
3. how to run data driven API Request?
4. how to run data driven tests?

## run a Collections Remotely
1. How to get Collection URL?
- get collection url by Share-get public link
2. How to run COllection remotely (from anywhere) using collection url?
- install newman and run with command
- `newman run https://www.getpostman.com/collections/04cb136837edf89cea19`

## How to run SOAP requests 
1. get SOAP request url or WSDL url add to request url
2. set method as POST
3. Set body as raw and set header text/xml
4. Provide request data body
- chrome plugin - Wizdler
5. Run and validata

## How to get value from Reponse and refer in Request | REST
- fetch data or value form response of one API and refer in another API
1. Add request in Postman
2. Use env variables to parameterize the value to be referred
3. Add scripts to fetch value from response of 1st API
4. Update the fetch va;ue in env veriables
5. Run and validate
ref:
- https://reqres.in/
- https://jsonpathfinder.com/

## API Authorization in Postman
- verify the identify
e.g. create repo on github by API which need login,otherwise will get response `401Unauthorized`
- create token on github and add token to Authorization Postman - Bearer Token




