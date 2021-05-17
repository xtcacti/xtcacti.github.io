---
title: test - GUI自动化测试篇
date: 2021-05-13 11:39:27
tags: test
---

# GUI 自动化测试
## 第一个 GUI 测试
1. Selenium的版本
- Selenium V1.0 的核心是Selenium RC
- Selenium V2.0 的核心是WebDriver
- Selenium V3.0 主要是增加了对MacOS的Safari和Windoews的Edge的支持，并彻底删除了对Selenium RC的支持
- Selenium V4.0 
2. Selenium V1.0 的原理
- 又称为Selenium RC（Remote Control）
- 原理是Javascript可以很方便的获取页面上的任何元素并执行各种操作
- 但是因为同源策略（只有来自相同域名、端口、协议的JavaScript代码才能被浏览器执行）
- 想要在测试用例运行中的浏览器注入JS代码从而实现自动化的Web操作，Selenium RC必须“欺骗”被测站点，让它误以为被注入的代码是同源的
- 如何实现“欺骗”？
  - 这就是引入Selenium RC Server的根本原因，其中Http Proxy模块就是用来“欺骗”浏览器的
- Selenium RC = Selenium RC Server + Selenium Client Library
  - Selenium RC Server = Launcher + HttpProxy + Selenium Core
    - Launcher：启动浏览器时完成Selenium Core的注入和浏览器代理的设置
    - HttpProxy：作为代理服务器修改JS的源，以达到欺骗被测站点的目的
    - Selenium Core：是被注入到浏览器中的JS函数的集合，用来实现界面元素的识别和操作
  - Selenium Client Library = Java/C#/Ruby/JS/Python...
    - Client Library是测试用例代码向Selenium RC Server发送Http请求的接口，支持多语言
3. Selenium V1.0 的执行流程
- 测试用例通过不同Client Library向Selenium RC Server发送Http请求，要求与其建立连接
- 连接建立后，RC Server的Launcher就会启动浏览器或重用已经打开的浏览器，把Selenium Core（JS函数集合）加载到浏览器页面当中，并同时把浏览器的代理设置为Http Proxy
- Client向RC Server发送Http请求，RC Server解析请求，并通过Http Proxy发送JS命令通知Selenium Core执行浏览器上控件的具体操作
- Selenium Core接收到指令后，执行具体操作
- 如果浏览器收到新的页面请求信息，则会发送Http请求来请求新的Web页面。由于Launcher在启动浏览器时把Http Proxy设置成了浏览器的代理，所以RC Server会接收到所有由它启动的浏览器的请求
- Selenium RC Server接收到浏览器发送的Http请求后，重组Http请求以规避同源策略，然后获取对应的Web页面
- Http Proxy会把接收到的web页面返回给利u蓝旗 ，浏览器对接收的页面进行渲染
4. Selenium V2.0 的原理
- 又称为Selenium WebDriver
- 原理是使用浏览器原生的WebDriver实现页面操作
- 典型的Server-Client模式
  - Server就是Remote Server
  - Client就是测试用例
5. Selenium V2.0 执行流程
- 当使用Selenium2.0启动浏览器时，后台会同时启动基于WebDriver Wire协议的Web Service作为Selenium的Remote Server，并与其浏览器进行绑定
- 绑定完成后，Remote Server开始监听Client端的操操作请求
- 执行测试时，测试用例会作为Client端，将需要执行的页面操作请求以Http Request的方式发送给Remote Server
- 该Http Request的body是以WebDriver Wire协议规定的JSON格式来描述需要浏览器执行的具体操作
- Remote Server接收到请求后，会对请求进行解析，并将请求结果发送给WebDriver，由WebDriver实际执行浏览器的操作
- WebDriver可以看作是直接操作浏览器的原生组件（Native Component），所以搭建huan'jinghuanjing 时，通常都需要下载浏览器对应的WebDriver
6. 其他GUI自动化测试框架
- UTF（以前的QTP）
- RFT
- Nightwatch

## 脚本与数据解耦 Page Object 模型
1. 数据驱动测试Data Drvien
- 解决了大量重复脚本的问题，实现了测试数据和脚本呢的解耦
- 支持csv、xls、json、yaml、甚至数据库的表
- 不仅可以支持测试的输入数据，也支持验证结果数据，或者逻辑分支的控制变量
- 数据驱动，不仅适用于GUI测试、也适用于API测试、单元测试
- 数据驱动往往是通过Test Data Provider模块将外部测试数据逐条喂给测试脚本
2. Page Object模型
- 将“流水账”般的测试脚本模块化为“可重用脚本的片段”
- 以页面（Web Page或者Native App Page）为单位来封装页面上的空间以及控件的部分操作
- 测试用例，也就是操作函数，基于页面封装对象来完成具体的操作，典型的模式时“XXXPage.YYYComponent.ZZZOperation”
  ```
  class LoginPage(){
      username_input = findElemntByName('username');
      passworde_input = findElemntByName('pwd');
      login_button = findElemntByName('login');
  }
  login(username,password){
      LoginPage.username_input(username);
      LoginPage.password_input(password);
      LoginPage.login_button.click();
  }
  ```
- 上面代码的方式就可以很方便的看出在什么页面执行什么操作

## 自动化测试脚本更好的描述业务
1. 把控操作函数的粒度：结合业务
2. 衔接两个操作函数之间的页面：页面跳转代码
3. 业务流程抽象
  - 业务流程的封装更接近实际业务
  - 基于业务流程的测试用例非常标准化，涉及“参数准备”、“实例化Flow”、“执行Flow”，非常适用于测试代码的自动生成
  - 由于更接近实际业务，所以很方便和BDD结合

## GUI 测试数据
1. 创建数据的方法
- API调用
- 数据库操作
- 两者结合

2. 创建数据的实践
- 实时创建 - On-the-fly：用于一次性使用的数据，保证不存在脏数据，比如：商品、订单、优惠券
- 提前创建 - Out-of-box：稳定的测试数据，比如：商品类型、图书类型

3. 数据创建工具？
## Page Code Gen + Data Gen + Headless
1. 页面对象自动生成技术
- 自动化你的自动化，只需要提供web页面的url，就可以生成整个页面的 所有控件的定位信息
- 但是依赖于数据的动态页面对象也会包含在自动生成的Page Class里，需要手动删除
- 商用自动化工具UFT已经支持自动化页面对象了
- 免费的Katalon Studio已经提供了类似的功能，可以试用

2. GUI测试数据自动生成
- 针对一个输入框，比如书名，就是string，那么就可以自动生成NULL、SQL注入、超长字符串、非英文字符串等等规则的测试数据
- 针对多个数据的组合，笛卡尔积的方式生成，手动剔除无效数据，结合实际情况使用

3. 无头浏览器Headless Browser
- 就是看不到界面的浏览器，截图依然可用
- 应用场景：GUI自动化测试、页面监控、网络爬虫
- 优点
  - 执行速度快，无需加载CSS以及渲染页面
  - 减少对测试执行的干扰，比如杀毒软件弹出框
  - 简化测试执行环境的搭建，减少对集群的依赖
  - 可以在单机环境实现测试的并发执行
- 缺点
  - 不能完全模拟真实用户的行为
  - 不适用于页面布局的校验


## GUI 稳定性
1. 不稳定因素
- 非预计弹窗框
  - 操作系统的弹窗框
  - 软件本身的弹窗框
  - 方案：
    - 异常场景恢复模式，处理已出现过的弹出框，出现弹出框进入异常模式，然后点掉弹出框，重新操作前面失败的步骤
    - 针对未出现的弹窗框，把框的详细信息（对象定位信息）更新到“异常场景恢复”库中，下次遇到相同的，就可以自动关闭了
- 页面控件的细微变化
  - 方案
    - 组合定位
    - 模糊匹配定位：建议引入规则引擎（好抽象，看不懂）
- 被测系统的A/B测试
  - 互联网产品常用的测试方法，为软件提供两个不同的版本，让用户随机访问其中一个，通过收集体验数据决定最终上线版本
  - 方案
    - 针对不同被测版本，对脚本作分支处理，脚本能够区分不同的版本
- 随机的页面延迟
  - 方案
    - retry机制：步骤级别、页面级别、业务级别都可，开源需二次开发
- 测试数据

## GUI 自动化测试报告
- 视频录制：体积大、分析也不方便
- 屏幕截图加高亮组合
1. Selenium WebDriver
- 扩展Selenium原本的操作函数
  - 比如click，不具备高亮，我们自己实现一个高亮的click
- 在相关的Hook操作中调用screenshot函数 
  - 在Hook里添加截图元素高亮以及任意额外操作（日志输出）
- 全球报告书的话，可以针对性的去涉及报告页面，方便比较
- 可以在报告中添加提交缺陷的按钮，直接提交到缺陷管理系统，大大提高了效率

## 大型项目 GUI 自动化测试策略e
- 把某模块涉及到的所有页面，按照页面对象模型的要求写生Pagee类
- 利用Page类进一步封装各自的业务流程脚本
- 再利用业务流程脚本进一步去实现GUI测试用例脚本
- 不同模块通过依赖与版本控制关联起来

## 移动应用测试方法思路
1. 移动端分类
- Web App：移动端web浏览器，依附的操作系统不再是Windows或Linux，而是iOS和Android，技术栈就是WEB技术，所访问的页面是放在服务器端额
  - 本质就是web浏览器页面的测试
- Native App：移动端的原生应用，Android(apk,Java),iOS(ipa,Objective-C)，基于手机操作系统，使用原生程序编写的第三方应用，可以提供比较好的用户体验和性能，并且可以方便的操作手机本地资源
  - 不同平台自动化测试方案不同（iOS->XCUITest | Android->UiAutomator2/Espresso）
- Hybird App：在原生应用中嵌入了WebView,维护简单、用户体验好、跨平台，是主流的移动应用开发模式
  - 上面两种的结合（Native Container和WebView是两个不同的上下文，前者是NATIVE APP，后者是WEBVIEW_+被测进程名称）

2. 移动应用专项测试的思路和方法
- 流量使用过多
- 耗电量过大
- 某些设备终端出现崩溃或闪退
- 多个移动应用互切，行为异常
- 在某些终端无法顺利安装或卸载
- 弱网络环境下无法使用
- Android环境下，经常出现ANR
- ...

3. 专项测试
- 交叉事件测试
  - 也称中断测试，在App执行过程中，有其他事件或应用中断当前应用执行的测试
  - 比如：电话、短信、闹钟、提示系统升级、低电量模式、第三方安全软件、网络切换、应用切换（都有音乐播放的功能）等
  - 目前都是在真机上进行手工测试，不会使用模拟器（只有真机才会出现，模拟器没有意义）
- 兼容性测试
  - 要确保App在各种终端、各种操作系统版本、各种屏幕分辨率、各种网络环境、功能的正确性
  - 同一种操作系统的不同语言环境也要覆盖
  - 不同网络环境包括（WIFI、GRPRS、EDGE、CDMA200）
  - 一台折别上与主流App的兼容性（微信、抖音、淘宝等）
  - 兼容性测试，通常都需要在各种真机上执行相同或类似的测试用例，所以往往采用自动化测试的手段
  - 由于需要覆盖大量的真实设备，
     - 大公司会采用Appium + Selenium Grid + Open STF去搭建自己的移动设备私有云平台
     - 小公司会采用第三方移动设备云平台完成兼容性测试（国外-SourceLab | 国内-Testin）
- 流量测试
  - 几方面
    - 首次下载安装包
    - 安装完成首次启动
    - App执行业务操作引起的流量
    - 后台运行
    - App内购买或者升级
  - 方案：
    - 流量测试往往借助于Android或iOS自带的流量统计，也可利用tcpdump、Wireshark、Fiddler等网络分析工具
    - Android：/proc/net/dev  | ADB工具 | Emmagee
    - iOS：Xcode自带的性能分析工具集Network Activity
  - 分析流量不是为了拿去相关数据，而是为了渐少流量
    - 数据压缩
    - 优化数据格式（JSON < XML）
    - 先压缩再加密
    - 减少单次GUI操作出发的后台调用数量
    - 回传数据只传必要的数据
    - 客户端缓存机制
- 耗电量测试
  - 几方面
    - App运行但没有执行业务
    - App运行且执行密集业务
    - App后台运行
  - 方案：
    - Android：`adb shell dumpsys battery`
    - iOS：Apple官方工具Sysdiagnose来手机耗电量信息，进一步通过Instrument工具链中的Energy Diagnostics进行耗电量分析
- 弱网测试
  - ATC（Facebook的Augmented Traffic Control）:可以模拟所有的网络需求
- 边界测试
  - 系统内存占用大于90%的场景
  - 系统存储占用大于95%的场景
  - 飞行模式来回切换的场景
  - App不具有某些权限的场景（不能访问相册、通讯录）
  - 长时间是使用App，系统资源是否正常（内存泄漏？）
  - 出现ANR场景
  - 操作系统事件早于或晚于标准时间的场景
  - 时区切换场景
  - ...


## Appium
1. 灵活性
- 支持多语言
- Appium Server支持多平台Windows/Mac
- 支持三大移动应用
- 支持iOS、Android
- 支持真机模拟器

2. 原理
- Appium Client：测试段代码基于JSON Wire协议的操作指令发送给Appium Server
- Appium Server：一个Node.js应用、接收来自Client的请求，解析后通过WebDriver协议和设备端上的代理打交道
  - iOS：Appium Server发给WDA（WebDriverAgent），WDA基于XCUITest完成iOS的自动化操作
  - Android：Appium Server把操作请求发送给appium-UIautomator2-server，然后再中转基于UIAutomator V2完成Android的自动化操作
- 设备端

> 声明：本站所有内容仅供个人学习娱乐笔记所用，如涉侵权，请联系删除