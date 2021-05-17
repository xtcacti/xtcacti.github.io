---
title: test - API自动化测试篇
date: 2021-05-14 14:13:37
tags: test
---

## API 测试 & 工具
1. 步骤
- 准备测试数据
- 通过API测试工具，发起对被测API的request
- 验证返回的response
2. 工具 
- 命令行cURL
- GUI的Postman、SoapUI
- API性能测试工具JMeter
3. cURL
- demo:`https://github.com/SpectoLabs/spring-cloud-contract-blog` 并启动account-service
- 下载cURL & 配置环境变量
- `curl -i -H "Accept: application/json" -X GET "http://127.0.0.1:8080/account/ID008"`
  - `-i`:要显示response的Header信息
  - `-H`:设定request中的Header
  - `-X`:用于指定执行的方法，默认是GET
  - `http://127.0.0.1:8080/account/ID008`：用于指明被测API的endpoint以及具体的ID值
  - `-d`：用于设定query string，也可以用&连接多个条件
  - `-b`：当需要传cookie时，指定cookie的文件路径
  - 大小写敏感
- `curl -i -H "sessionid:XXXXXXXXXX" -X GET "http://XXX/api/demoAPI"`
  - 后端传给前端一个session，前端在发给后端的request中的header中就要指定session，后端才能知道前端属于哪个session
- ```
   // 将cookie保存为文件
   curl -i -X POST -d username=robin -d password=password123 -c ~/cookie.txt "http://XXX/auth"

   // 载入cookie到request中
   curl -i -H "Accept:application/json" -X GET -b ~/cookie.txt "http://XXX/api/demoAPI"
   ```
  - 使用cookie，在认证成功后，后端会返回一个cookie给前端，前端可以把cookie保存成我呢见，使用时，用`-b cookie_file`植入到request中即可
- cURL只能发起API调用，而其本身不具备结果验证的能力，所以实际意义上cURL并不属于测试工具的范畴


4. Postman

5. 复杂场景的API测试
- 实现API的调用和结果的解析的代码化，可以灵活的直接用代码来处理这些场景
  - 通过代码将上个API返回的response中的某个值传递给下一个API，再根据上一个API的返回结果决定下一个应该调用哪个API
- 如何才能高效获取单个前端操作所触发的API调用机制
  - 通过网络监控的手段，捕获单个前端操作所触发的API调用序列
  - 比如，通过Fiddler之类的网络抓包工具，获取这个调用序列
  - 比如，很多互联网公司在考虑基于用户行为日志，通过大数据手段获取序列
- API测试过程中的第三方依赖
  - API之间是存在依赖关系的，比如你的被测对象时API A，但是API A的内部调用了API B，API B此时又不可用，那么API A的测试就受影响
  - 单体架构下，这种问题只存在于涉及到第三方API依赖时，还是小事
  - 微服务架构下，API之间互相耦合的依赖问题就会非常严重了
    - 解决方案：用Mock Server来代替真实的API
- 异步API测试
  - 异步API测试指的是，调用后会立即返回，但是实际任务并没有真正完成，而是需要稍后去查询或者回调Callback的API
  - 异步测试主要分两部分
    - 测试异步调用是否成功：检查返回值和后台工作线程是否被创建
    - 测试异步调用的业务逻辑是否正确：异步API通常发生在比较慢的操作上，比如数据库I/O、消息队列I/O，此时测试往往需要去验证数据库中的值、消息队列中的值，这就需要测试代码具有访问和操作数据库或消息队列的能力，实际工作中要求API测试框架具有工具类访问和操作数据库或者消息队列

## API 自动化测试框架的前世今生
1. 早期的基于Postman的API测试
- ∵ 基于界面，遇到瓶颈
  - 当需要频繁执行大量的测试用例，基于界面的API测试就显得笨拙
  -  基于界面的测试难以与CI/CD流水线集成
- ∴ 迫切需要一个基于命令行执行的的API测试方案

2. 基于Postman和Newman的API测试
- 用Postman开发调试测试用例，完成后通过Newman执行
- ∵ 看似完美的方案，但是实际工程中存在连续调用多个API的情况，涉及到API调用时的数据传递问题，还会遇到API调用前需要执行一些特定的操作（准备测试数据）
- ∴ 仍旧不完美

3. 基于代码的API测试
- 基于Java的OkHttP & Unirest
- 基于Python的http.client & Requests
- 基于NodeJS的Native & Request
- 小公司会选用这些成熟的API测试框架
- 大公司会结合自己的业务上下文，开发自己的HttpClient，封装全新的RestAssured
  - 可以灵活支持多个API的顺序调用
  - 可以做一些类似BeforeHook（数据准备）、AfterHook（清理工作）的工作
  - 可以很方便的做数据驱动
  - 由于直接采用了代码实现，可以更灵活的处理断言
  - 原生支持命令行，方便集成
- ∵又遇到了瓶颈
  - 对于单个API测试的场景，工作量相比Postman大得多
  - 对于单个API测试的场景，无法重用Postman里面已经积累的Collection
  - 实际工作中，这两点非常重要，必须解决，老板不会接受相同工作的量直线上升、完成的部分无法使用原本已经
- ∴ 自动化生成API的测试代码的技术应运而生

4. 自动生成API代码
- 基于Postman的Collection生成基于代码的API测试用例
- ∵ Postman本身支持将Collection转换为测试代码，但仍有问题
  - 断言部分不会生成代码
  - 中大型互联网公司都是用自己开发的API测试框架，那么测试代码就会和自研的API测试框架绑定在一起，显然Postman并不支持这类代码的自动生成
- ∴ 理想的是自己实现一个代码自动生成工具，输入是Postman中Collection的JSON文件，输出是基于自研API框架的测试代码，而且同时会把测试的断言一并转换为代码
- 方案：
  - 根据自研API框架的代码结构建立一个带有变量占位符的模板文件
  - 通过JSON解析程序，按照Collection JSON文件的格式定义去提取header、method等信息
  - 用提取到的具体值替换之前模板文件中的变量占位符，就得到了自研框架的API测试用例代码
- Working Model
  - 对于Postman中已经积累的Collection，全部由这个工具统一转换为基于代码的API测试用例
  - 开发人员继续使用Postman执行基本的测试，并将所有的测试用例保存成Collection，后续由统一工具换成基于代码的API测试用例
  - 对于复杂测试场景（顺序调用多个API测试），可以组装成由工具转换得到的API测试用例代码，完成测试工作
- BUT 仍旧有痛点，就是测试验证中的断言 

5. Response结果发生变化时的自动识别
- 迫切需要一个方法，既可以不对所有的字段去写assert，又可以检测到response的结构以及没有写assert的字段值的变化
- 思路：
  - 在API测试框架里引入一个内建数据库，推荐NoSQL（MongoDB），这个数据库记录每次调用的request和response的组合，当下次再发送相同的request时，API测试框架会自动和上次的response做差异检测，对于变化的字段给出警告。
  - 针对每次都变化的值，比如（token、sessionId、时间戳）等，可以通过规则配置设立一个白名单列表，把动态值排除在外

## 微服务模式下的API测试怎么做
- 微服务架构下的最大挑战就是庞大的测试用例数量以及微服务之间的相互耦合，首先要了解什么是微服务，对比之下要先了解什么是单体架构
1. 单体架构（Monolithic Architecture）
- 单体架构是早期的架构模式，并且存在了很长时间
- 单体架构是将所有的业务场景的表示层、业务逻辑层和数据访问层放在同一个工程中，最终经过编译、打包、并部署在服务器上
- e.g.经典的J2EE工程就是将表示层的JSP、业务逻辑层的Service、Controller和数据访问层的DAO（Data Access Objects），打包成war文件，然后部署在Tomcat、Jetty或者其他Servlet容器中运行
- 优点：发布简单、方便调试、架构复杂性低
- ∴ 长期以来被广泛使用，广泛应用于传统企业软件
- 缺点：随着互联网的普及，应用所承载的流量越来越大，单体架构的问题也逐渐被暴露并不断放大
  - 灵活性差：无论是多小的修改，也要打包发布整个应用，花费时间大
  - 可扩展性差：在高并发模式下，无法以模块为单位灵活扩展容量，不利于应用的横向扩展
  - 稳定性差：当单体中任何一个模块有问题，都可能会导致应用整体的不可用，缺乏容错机制
  - 可维护性差：业务复杂度up，代码复杂度up，维护性down
- ∴ 面对互联网，单体架构有一道无法逾越的鸿沟
- ∴ 催生了SOA架构、微服务架构

2. 微服务架构（Microservice Architecture）
- 微服务是一种架构风格
- 在微服务架构下，一个系统不再是由一个单体组成，而是由一系列相互独立的微服务组成
- 各个微服务运行在自己的进程中，开发和部署都没有依赖
- 不同服务之间通过一些轻量级交互机制进行通信（RPC、HTTP）
- 微服务可独立扩展伸缩，每个服务定义了明确的边界，只需要关注并很好的完成一件任务就可以了
- 不同的服务可以根据实现的便利性采用不同的编程语言实现，由独立的团队来维护
- 优点
  - 每个服务运行在独立的进程中，开发技术栈也可独立
  - 服务间采用轻量级通信，通常是基于HTTP的Restful API
  - 每个服务围绕具体业务，独立开发、独立部署，独立发布
  - 对运维提出了较高的要求，促成了CI/CD的发展与落地

## 微服务下的测试挑战
### 庞大的测试用例
1. 传统API测试策略（单体）
- 根据被测API输入参数各种组合调用API，验证结果
- 衡量上述测试中的代码覆盖率
- 以代码覆盖率作为API测试成功完成的标志
- e.g. 单体系统对外提供了3个Restful API，那么测试策略只需要针对这3个API设计用例，执行，补充，完成

2.微服务下 
- e.g. 微服务下，系统被拆分成了10个service，每个service平均暴露3个接口，总共就要测30个接口数量
- 用力数量多，测试时间少
- ∴ 引入了基于消费者契约的API测试

### 微服务之间的耦合关系
- 被测对象Service T，Service T又依赖Service X和Service Y，被依赖的若处于不可用状态，那么T也无法完成测试
- ∴ 需要想办法接触T 与 X、Y之间的耦合关系，也就是解耦
- 方案
  - 采用Mock Service来代替真实的Service（消费者契约API测试）

## 基于消费者契约的API测试
- Service T的消费者是Service X，Service Y
- 要测试T，传统就是找到所有的参数组合依次对T进行调用，然后结合代码覆盖率进行补充
- 测试用例特别多的话，怎么提高效率
  - 思路：T的消费者只有X，Y，那么测T，可以转变成测X，Y所有可能对T的调用，找到这样的调用集合，作为T的测试用例即可
  - 方案：
    - 理论上：在逻辑结构上，在T前面放一个代理，所有进出T的Requests和Responses都经过这个代理，并被记录成JSON文件，也就构成了契约
    - 实际项目上：不可能每一个Service都放置一个代理，但是微服务架构下往往会有一个API Gateway的组件，用于记录所有API之间相互调用关系的日志，通过解析日志得到Service的契约
- ∴ 这就是基于消费者契约的API测试

## 微服务下测试的依赖解耦 & Mock Service
- 实现Mock Service的关键就是能够模拟被替代Service的Request和Response
- 通过消费者契约已经拿到了契约，也就是Request和Response的组合（JSON文件），可以作为Mock Service的依据，收到什么Request，返回什么Response
- 由此达到解耦

## Ref(沒看懂啊)
- https://github.com/SpectoLabs/spring-cloud-contract-blog
- https://specto.io/blog/2016/11/16/spring-cloud-contract/

> 声明：本站所有内容仅供个人学习娱乐笔记所用，如涉侵权，请联系删除