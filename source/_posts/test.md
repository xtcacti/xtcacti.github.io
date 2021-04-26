---
title: test
date: 2021-04-19 20:43:12
tags: test
---

# 软件测试基础篇

## ------------------

## 从用户登录谈起

1. 用户登录 <不及格版>

- 输入用户名密码
- 点击登录
- 验证是否登陆成功

2. 但是，作为测试工程师，要保证系统在各个应用场景下的功能是符合设计要求的，所以需要设计更多更全面的测试用例

- 等价类划分
  - 将所有可能输入的数据划分为若干个子集，每一个子集的任何一个数据对于揭露程序中存在的典型错误都有同等效果，那么一个子集就是一个等价类。在测试时，一个子集选取一个数据就可以用少量具有代表性的测试输入取得较好的测试覆盖结果
- 边界值分析
  - 选取输入、输出值的边界值进行测试。通常大量的软件错误发生在输入或输出的范围边界上，所以需要对边界值进行重点测试。比如选取正好等于、刚刚大于或小于的边界值作为测试数据。
- 等价类划分和边界值分析都属于典型的黑盒测试方法。边界值分析法正好是对等价类划分的补充，所以通常结合起来使用。

3. 用户登录测试用例优化：<及格版>

- 输入已注册用户名和正确密码登录 -> 验证是否登录成功；
- 输入已注册用户名和不正确的密码登录 -> 验证是否失败，并提示信息正确
- 输入未注册用户名和任意密码 -> 验证是否失败，并提示信息正确
- 用户名密码都为空 -> 验证是否失败，并提示信息正确
- 用户名密码之一为空 -> 验证是否失败，并提示信息正确
- 若有验证码，输入正确用户名密码，正确验证码 -> 验证是否登录成功
- 若有验证码，输入正确用户名密码，不正确验证码 -> 验证是否登录失败，并提示信息正确

4. 用户登录测试用例 zai 优化：<良好版> 显性功能完整了

- 用户名密码是否大小写敏感
- 页面密码框是否加密显示
- 后台系统创建的用户，第一次登陆成功，是否提示修改密码
- 忘记用户名和忘记密码功能是否可用
- 前端页面是否根据设计要求对用户名密码限制长度
- 如果有验证码，点击验证码图片是否会更新验证码，更新后的验证码是否可用
- 刷新页面是否会刷新验证码
- 如果验证码有时效性，需要对时效内和时效外的验证码分别做校验
- 用户登陆成功后，会话超时，是否会重定向到用户登录页面
- 不同级别的用户，比如管理员和普通用户，登录系统后的权限是否正确
- 页面默认聚焦是否定位在用户名的输入框中
- 快捷键 tab 和 enter 是否可以正常使用
  - 所谓显性就是肉眼可见的功能测试，以上用例都是基于显性的功能测试，质量过硬的软件系统，除了显示的 功能需求外，还有非功能性需求即隐形需求。
  - 非功能性需求：
    - 安全性、
    - 性能、
    - 兼容性
  - 非功能性需求测试，往往正是决定软件质量的关键

5. 用户登录测试用例 zai 优化：<优秀版> 隐性功能完整了

- 安全性：
  - 用户密码后台存储是否加密
  - 用户密码在网络传输过程中是否加密
  - 密码是否具有时效性，密码到期后是否提示修改密码
  - 不登陆的情况下，在浏览器中直接输入登陆后的 url，是否会直接重定向到用户登录界面
  - 密码输入框是否不支持复制和粘贴
  - 密码输入框输入的密码是否都可以在页面源码模式下被查看
  - 用户名和密码的输入框分别输入典型的`SQL注入攻击`字符串,验证系统返回界面
  - 用户名和密码输入框分别输入典型的`XSS跨站脚本攻击`字符串，验证系统行为是否被篡改
  - 连续多次登录失败之后，系统是否会阻止后续的尝试以应对暴力破解
  - 同一用户在同一终端的多种浏览器登录，验证登录功能的互斥性是否符合设计预期
  - 同一用户先后在多台终端的浏览器登录，验证登录时候具有互斥性
- 性能测试：
  - 单用户登录的响应时间是否小于 3 秒
  - 单用户登录，后台请求数量是否过多
  - 高并发场景下用户登录的响应时间是否小于 5 秒
  - 高并发场景下，服务端的监控指标是否符合预期
  - 高集合点并发场景下，是否存在资源死锁和不合理的资源等待
  - 长时间大量用户连续登录和登出，服务器端是否存在内存泄漏
- 兼容性测试
  - 不同的浏览器下，验证登陆页面的显示功能是否正确
  - 相同浏览器的不同版本，验证登陆页面的显示功能是否正确
  - 不同的移动终端的不同浏览器下，...
  - 不同的分辨率界面下，...

6. 测试之路，遥遥无期，没有穷尽(穷尽测试),但实际工作，由于时间程本和经济成本，无法完成穷尽测试，所以采用基于风险驱动模式，有所侧重的选择测试范围和设计测试用例，寻求缺陷风险和研发成本之间的平衡。

7. 登录补充用例：

- 网络延迟、弱网络、切换网络、断网时是否能正常登录
- 是否支持第三方登录
- 是否可以记住密码（密码有效期过了，是否会清除密码）
- 是否支持特殊字符和中文
- 是否可以使用登录的 API 发送登录请求，并绕开验证码校验
- 是否可以用抓包工具抓到的请求包直接登录
- 截取到的 token 等信息，是否可以在其他终端直接使用，绕开登录，token 过期时间校验
- 登录后输入登录的 URL 之后，是否还能再次登录

## 如何设计一个“好的”测试用例

- 池塘捕鱼 傻子吃大饼

1. 好的测试用例的特点：

- 整体完备性
- 等价类划分的准确性
- 等价类划分的完备性

2. 三种常用的软件测试方法
   学生信息系统的考试成绩输入项 0-100 分的范围

- 等价类划分
  - 有效等价类：0~59 59~100
  - 无效等价类：小于 0 大于 100 0~100 之间的浮点数 非数字
- 边界值分析 对等价类划分的补充
  - -1 0 1 59 60 61 99 100 101
- 错误推测
  - 基于对被测软件系统设计的理解，结合个人经验直觉，推测书软件可能存在的缺陷，从而针对性的设计测试用例方法，过度依赖个人能力
  - 与探索是测试方法的基本思想和理念不谋而合，这个方法在敏捷开发模式下投入产出比很高
  - e.g.
    - Web GUI 功能测试需要考虑浏览器在有缓存无缓存下的表现
    - Web Service API 测试考虑被测 API 所依赖的第三方 API 出错下的处理逻辑
    - 代码级单元测试，需要考虑被测函数输入为空的情况下的内部处理逻辑
  - 企业为了降低对个人能力的依赖，一般会维护缺陷知识库，对中小企业就是建立简单的 wiki 页面，手动补充
  - 对于测试基础架构比较成熟的中大型软件企业，通常会以该缺陷知识库作为数据驱动测试的输入来自动生成部分的测试数据

3. 真正的工程实践中，不同的软件项目在研发生命周期的各个阶段都有不同的测试类型

- 开发阶段 - 单元测试
- 软件模块集成阶段 - 代码继承测试
- 打包部署后 - 面向终端用户的 GUI 测试
- 电商网站 - 服务器端基于 API 的测试、中间件测试、GUI 测试等等

4. 用例设计的其他经验

- 只有深入理解被测软件的架构，才能设计出有的放矢的用例集，去发现系统边界以及系统集成上的潜在缺陷
  - 一定不能把被测系统看成一个大黑盒，必须对内部的架构有清楚的认识，比如数据库的连接方式、数据库的读写分离、消息中间件 Kafka 的配置、缓存系统的层级分布、第三方系统的集成
- 必须深入理解被测软件的设计与实现细节，深入理解软件内部的处理逻辑
  - 处理流程、分支处理，可以通过代码覆盖率指标找出可能的测试遗漏点
  - 不要以开发代码的实现作为依据去设计用例，否则可能会错上加错
  - 要以原始需求去设计测试用例
- 可以引入需求覆盖率和代码覆盖率来衡量测试执行的完备性，并以此为依据找出测试点

## 单元测试

1. what

- 单元测试是指，对软件中最小的可测试单元在与其他程序相分离的状态下进行检查和验证，通常指函数和类。
- 一般开发来做，保证在最早期以最小成本来保证局部代码的质量
- 通常都是自动化执行

2. how
   驱动代码？桩代码？Mock 代码？

- 代码的基本特征与产生错误的原因
  - 条件分支、循环处理、函数调用
  - 任何一个分类遗漏、分类错误、分类逻辑错误都会产生缺陷
  - 开发设计逻辑功能正确的代码时会思考：
    - 哪几种正常的输入 - 等价类划分思想
    - 特殊的边界输入 - 边界分析思想
    - 潜在非法输入的处理 - 错误推测思想
- 单元测试用例详解
  - 单元测试的用例是一个“输入数据”和“预计输出”的集合
  - 输入数据：
    - 被测函数的输入参数
    - 被测函数内部需要读取的全局静态变量
    - 被测函数内部需要读取的成员变量
    - 函数内部调用子函数获得的数据
    - 函数内部调用子函数改写的数据
    - 嵌入式系统中，在中断调用时改写的数据
    - ...
  - 预计输出：
    - 被测函数的返回值
    - 被测函数的输出参数
    - 被测函数所改写的成员变量
    - 被测函数所改写的全局变量
    - 被测函数中进行的文件更新
    - 被测函数中进行的数据库更新
    - 被测函数中进行的消息队列更新
    - ...
- 驱动代码、桩代码、Mock 代码
  - 驱动代码时是用来调用被测函数的
  - 桩代码和 Mack 代码是用来替代被测函数调用的函数的一个临时代码
- 单元测试选型：
  - Java - Junit/TestNG
- 桩代码、Mock 代码选型工作是由开发架构师和测试架构师共同决定的
- 为了衡量单元测试代码覆盖率，引入代码覆盖率工具
  - Java - JaCoCo
- 最后需要把单元测试执行、代码覆盖率统计和持续集成流水线集成，以确保每次代码递交，都会自动触发单元测试，并在单元测试执行过程中自动统计代码覆盖率，最后以单元测试通过率和代码覆盖率为标准来决定本次代码递交是否能够被接受。
- 单元测试困难需克服：
  - 紧密耦合代码难以隔离
  - 隔离后编译链接运行困难
  - 代码本身可测试性差
  - 无法通过桩代码直接模拟底层函数的调用
  - 代码覆盖率越往后越难以提高

## 自动化测试

1. what

- 人对软件测试的行为 -> 机器对软件测试的行为
- 若自动化测试用例维护成本高于其节省的测试成本时，自动化测试就失去了价值与意义

2. why

- 可替代手工机械重复性工作
- 大幅提升回归测试效率，非常适合敏捷开发过程
- 可利用无人值守时间，去频繁执行测试，非工作时间执行测试，工作时间分析报告
- 可完成非常巨大的测试类型，比如关键业务 7\*24 小时持续运行的系统稳定性测试和高并发场景下的压力测试等
- 可保证每次测试执行的操作及验证的一致性和可重复性，避免人为遗漏或疏忽
- ======BUT======
- 脆弱，无法应对系统的变化 ->开发手一抖，自动化测试忙一宿
- 自动化测试程本 = 单词手工测试\*5
- 自动化测试紧紧能发现回归测试的缺陷
- 业务测试专家和自动化测试专家通常是两批人，只有紧密合作，才能高效开展
- 编程能力

3. when

- 需求稳定，不会频繁变更
- 研发和维护周期厂，需频繁执行回归测试
- 软件产品比软件项目更适合，因为产品是一个迭代的过程，迭代就需要回归测试
- 对于软件项目，考虑用 20%的精力覆盖 80%的回归测试，其他功能尽量用探索式测试
- 需要在多个平台上重复运行相同测试的场景
  - 不同浏览器
  - 不同浏览器的不同版本，安卓、IOS 的不同版本
  - 不同客户的不同定制版本，主体功能一致
- 对某些测试项目通过手工无法实现，手工成本太高
  - 性能和压力测试
  - e.g. 一万用户并发量 | 7\*24 小时稳定性测试
  - 就需要基于协议的自动化测试技术了
- 被测软件规范，具有可测试性
  - 比如，GUI 测试的定位元素若无规则可循就没法弄了
  - 验证码需要开发预留测试性接口，否则就只能借助光学字符识别（OCR）技术来对图片验证码进行技术识别，不稳定
- 编程能力
  - 编程学习时间长
  - tester 对自动化测试技术一腔热血，忽略了测试用例的设计，直接影响整体质量

## 各个阶段的自动化测试技术

1. 单元测试自动化技术

- 用例框架代码生成的自动化：TestNG
- 部分测试输入数据自动化生成
- 自动桩代码生成
- 被测代码的自动化静态分析:SOnar Coverity 编码规则规范
- 测试覆盖率的自动统计与分析：自动化工具自动统计各种测试覆盖率

2. 代码级集成自动化技术

- 基本不做

3. WebService 自动化技术

- 就是针对 SOAP API 和 REST API 这两类 API 测试，最典型的就是用 SoapUI 或 Postman 等工具。但这类工具都是界面操作手动发起的 Request 并验证 Response，难以和 CI/CD 集成，于是就出现了 API 自动化测试框架。
- e.g. REST Assured
- 基于代码的 API，包含三大步骤：
  - 测试数据
  - 调用参数并发起 API 调用
  - 验证返回结果
- 测试脚手架代码的自动化生成
- 部分测试输入数据的自动化生成
- Response 验证的自动化
- 基于 SOAPUI 或者 Postman 的自动化脚本的生成
  - 自己实现一个工具，输入时 SOAPUI 或 Postman 的用例元数据，输出是基于 diamagnetic 实现的测试用力了

## GUI 自动化

- Web
  - Selenium(Open Source)
  - Micro FOcus 的 UFT(前身 QTP) (Bussiness Edition)
- Native App
  - Appium
    - iOS:集成 XCUITest
    - Android：集成 UIAutomator 和 Espresso

## 测试覆盖率
### 需求覆盖率：面向需求
- 将每一条软件需求和对应的测试建立一对多的映射关系，最终目标是保证测试可以覆盖每个需求，以保证软件产品的质量。
- 
### 代码覆盖率：面向技术

## 高效填写软件缺陷报告

## 做好测试计划

## 软件测试工程师的核心竞争力

## 软件测试工程师需要掌握的非测试知识

## 互联网产品测试策略设计

# GUI 自动化测试

## ------------------

## 第一个 GUI 测试

## 脚本与数据解耦 Page Object 模型

## 自动化测试脚本更好的描述业务

## GUI 测试数据

## Page Code Gen + Data Gen + Headless

## GUI 稳定性

## GUI 自动化测试报告

## 大型项目 GUI 自动化测试策略

## 移动应用测试方法思路

## Appium

# API 自动化测试

## ------------------

## API 测试 & 工具

## API 自动化测试框架

## 微服务模式下的 API 测试

# 代码测试

## ------------------

## 代码测试的理念 & 方法

## 静态测试方法

## 动态测试方法

# 性能测试

## ------------------

## 软件性能 & 性能指标

## 性能测试基本方法 & 应用领域

## 后端性能测试工具 & 工具原理

## 前端性能测试工具 & 工具原理

## LoadRunner 企业级服务器端性能测试

## 企业级实际性能测试

# 测试数据准备

## ------------------

## 如何准备测试数据

## 测试数据的痛点

## 统一测试数据平台

# 测试基础架构

## ------------------

## Selenium Grid

## 测试环境架构设计

## 大型电商测试基础架构设计

# 测试新技术

## ------------------

## 探索是测试

## 测试驱动开发(TDD)

## 精准测试

## 渗透测试

## 基于模型的测试

# 测试人员互联网架构核心知识

## ------------------

## 为啥摇动大型网站架构设计

## 网站高性能架构设计

## 网站高可用架构设计

## 网站可扩展性架构设计