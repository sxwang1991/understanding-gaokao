[✔]: 041423430593_1.svg

# 二零一五至二零一九年高考数学试题分析

<h1 align="center">
  <img src="assets/images/banner-2.jpg" alt="高考数学试题分析" />
</h1>

<br/>

<div align="center">
  <img src="041423430593_1.svg" alt="82 items"> <img src="041423430593_2.svg" alt="Last update: June 5, 2019"> <img src="041423430593_3.svg" alt="Updated for Node 12.4.0 LTS">
</div>

<br/>

 [![nodepractices](/assets/images/twitter-s.png)](https://twitter.com/nodepractices/) **Follow us on Twitter!** [**@nodepractices**](https://twitter.com/nodepractices/)
 <br/>

# 欢迎! 首先您应该知道的三件事情:
**1. 当您读到这里，实际上您读了很多关于Node.js的优秀文章 -** 这是对Node.js最佳实践中排名最高的内容的总结和分享

**2. 这里是最大的汇集，且每周都在增长 -** 当前，超过50个最佳实现，样式指南，架构建议已经呈现。每天都有新的issue和PR被创建，以使这本在线书籍不断更新。我们很乐于见到您能在这里做出贡献，不管是修复一些代码的错误，或是提出绝妙的新想法。请查看我们的[milestones](https://github.com/i0natan/nodebestpractices/milestones?direction=asc&sort=due_date&state=open)

**3. 大部分的条目包含额外的信息 -** 大部分的最佳实践条目的旁边，您将发现 **🔗Read More** 链接，它将呈现给您示例代码，博客引用和更多信息

<br/><br/><br/>

## [目录](#table-of-contents)
1. [项目结构实践 (5) ](#1-project-structure-practices)
2. [异常处理实践 (11) ](#2-error-handling-practices)
3. [编码规范实践 (12) ](#3-code-style-practices)
4. [测试和总体质量实践 (8) ](#4-testing-and-overall-quality-practices)
5. [进入生产实践 (16) ](#5-going-to-production-practices)
6. :star: 新: [安全实践(23)](#6-security-best-practices)
7. Performance Practices ([coming soon](https://github.com/i0natan/nodebestpractices/milestones?direction=asc&sort=due_date&state=open))


<br/><br/><br/>
<h1 id="1-project-structure-practices"><code>1. 项目结构实践</code></h1>

## ![✔] 1.1 组件式构建你的解决方案

 **TL;DR:** 大型项目的最坏的隐患就是维护一个庞大的，含有几百个依赖的代码库 - 当开发人员准备整合新的需求的时候，这样一个庞然大物势必减缓了开发效率。反之，把您的代码拆分成组件，每一个组件有它自己的文件夹和代码库，并且确保每一个组件小而简单。查看正确的项目结构的例子请访问下面的 ‘更多’ 链接。

**否则:** 当编写新需求的开发人员逐步意识到他所做改变的影响，并担心会破坏其他的依赖模块 - 部署会变得更慢，风险更大。当所有业务逻辑没有被分开，这也会被认为很难扩展

🔗 [**更多: 组件结构**](/sections/projectstructre/breakintcomponents.chinese.md)

<br/><br/>

## ![✔] 1.2 分层设计组件，保持Express在特定的区域

**TL;DR:** 每一个组件都应该包含'层级' - 一个专注的用于接入网络，逻辑，数据的概念。这样不仅获得一个清晰的分离考量，而且使仿真和测试系统变得异常容易。尽管这是一个普通的模式，但接口开发者易于混淆层级关系，比如把网络层的对象（Express req, res）传给业务逻辑和数据层 - 这会令您的应用彼此依赖，并且只能通过Express使用。

**否则:** 对于混淆了网络层和其它层的应用，将不易于测试，执行CRON的任务，其它非-Express的调用者无法使用

🔗 [**更多: 应用分层**](/sections/projectstructre/createlayers.chinese.md)

<br/><br/>

## ![✔] 1.3 封装公共模块成为NPM的包

**TL;DR:** 由大量代码构成的一个大型应用中，贯彻全局的，比如日志，加密和其它类似的公共组件，应该进行封装，并暴露成一个私有的NPM包。这将使其在更多的代码库和项目中被使用变成了可能。

**否则:** 您将不得不重造部署和依赖的轮子

🔗 [**更多: 通过需求构建**](/sections/projectstructre/wraputilities.chinese.md)

<br/><br/>

## ![✔] 1.4 分离 Express 'app' and 'server'

**TL;DR:** 避免定义整个[Express](https://expressjs.com/)应用在一个单独的大文件里， 这是一个不好的习惯 - 分离您的 'Express' 定义至少在两个文件中： API声明(app.js) 和 网络相关(WWW)。对于更好的结构，是把你的API声明放在组件中。

**否则:** 您的API将只能通过HTTP的调用进行测试（慢，并且很难产生测试覆盖报告）。维护一个有着上百行代码的文件也不是一个令人开心的事情。

🔗 [**更多: 分离 Express 'app' and 'server'**](/sections/projectstructre/separateexpress.chinese.md)

<br/><br/>

## ![✔] 1.5 使用易于设置环境变量，安全和分级的配置


**TL;DR:** 一个完美无瑕的配置安装应该确保 (a) 元素可以从文件中，也可以从环境变量中读取 (b) 密码排除在提交的代码之外 (c) 为了易于检索，配置是分级的。仅有几个包可以满足这样的条件，比如[rc](https://www.npmjs.com/package/rc), [nconf](https://www.npmjs.com/package/nconf) 和 [config](https://www.npmjs.com/package/config)。

**否则:** 不能满足任意的配置要求将会使开发，运维团队，或者两者，易于陷入泥潭。

🔗 [**更多: 配置最佳实践**](/sections/projectstructre/configguide.chinese.md)

<br/><br/><br/>

<p align="right"><a href="#table-of-contents">⬆ 返回顶部</a></p>

<h1 id="2-error-handling-practices"><code>2. 错误处理最佳实践</code></h1>

## ![✔] 2.1  使用 Async-Await 和 promises 用于异步错误处理

**TL;DR:** 使用回调的方式处理异步错误可能是导致灾难的最快的方式(a.k.a the pyramid of doom)。对您的代码来说，最好的礼物就是使用规范的promise库或async-await来替代，这会使其像try-catch一样更加简洁，具有熟悉的代码结构。

**否则:** Node.js回调特性, function(err, response), 是导致不可维护代码的一个必然的方式。究其原因，是由于混合了随意的错误处理代码，臃肿的内嵌，蹩脚的代码模式。

🔗 [**更多: 避免回调**](/sections/errorhandling/asyncerrorhandling.chinese.md)

<br/><br/>

## ![✔] 2.2 仅使用内建的错误对象

**TL;DR:** 很多人抛出异常使用字符串类型或一些自定义类型 - 这会导致错误处理逻辑和模块间的调用复杂化。是否您reject一个promise，抛出异常或发出(emit)错误 - 使用内建的错误对象将会增加设计一致性，并防止信息的丢失。


**否则:** 调用某些模块，将不确定哪种错误类型会返回 - 这将会使恰当的错误处理更加困难。更坏的情况是，使用特定的类型描述错误，会导致重要的错误信息缺失，比如stack trace！

🔗 [**更多: 使用内建错误对象**](/sections/errorhandling/useonlythebuiltinerror.chinese.md)

<br/><br/>

## ![✔] 2.3 区分运行错误和程序设计错误

**TL;DR:** 运行错误（例如, API接受到一个无效的输入）指的是一些已知场景下的错误，这类错误的影响已经完全被理解，并能被考虑周全的处理掉。同时，程序设计错误（例如，尝试读取未定义的变量）指的是未知的编码问题，影响到应用得当的重启。

**否则:** 当一个错误产生的时候，您总是得重启应用，但为什么要让 ~5000 个在线用户不能访问，仅仅是因为一个细微的，可以预测的，运行时错误？相反的方案，也不完美 – 当未知的问题（程序问题）产生的时候，使应用依旧可以访问，可能导致不可预测行为。区分两者会使处理更有技巧，并在给定的上下文下给出一个平衡的对策。

🔗 [**更多: 运行错误和程序设计错误**](/sections/errorhandling/operationalvsprogrammererror.chinese.md)

<br/><br/>

## ![✔] 2.4 集中处理错误，不要在Express中间件中处理错误

**TL;DR:** 错误处理逻辑，比如给管理员发送邮件，日志应该封装在一个特定的，集中的对象当中，这样当错误产生的时候，所有的终端（例如 Express中间件，cron任务，单元测试）都可以调用。

**否则:** 错误处理的逻辑不放在一起将会导致代码重复和非常可能不恰当的错误处理。

🔗 [**更多: 集中处理错误**](/sections/errorhandling/centralizedhandling.chinese.md)

<br/><br/>

## ![✔] 2.5 对API错误使用Swagger文档化

**TL;DR:** 让你的API调用者知道哪种错误会返回，这样他们就能完全的处理这些错误，而不至于系统崩溃。Swagger，REST API的文档框架，通常处理这类问题。

**否则:** 任何API的客户端可能决定崩溃并重启，仅仅因为它收到一个不能处理的错误。注意：API的调用者可能是你（在微服务环境中非常典型）。


🔗 [**更多: 使用Swagger记录错误**](/sections/errorhandling/documentingusingswagger.chinese.md)

<br/><br/>

## ![✔] 2.6 当一个特殊的情况产生，停掉服务是得体的

**TL;DR:** 当一个不确定错误产生（一个开发错误，最佳实践条款#3) - 这就意味着对应用运转健全的不确定。一个普通的实践将是建议仔细地重启进程，并使用一些‘启动器’工具，比如Forever和PM2。

**否则:** 当一个未知的异常被抛出，意味着某些对象包含错误的状态（例如某个全局事件发生器由于某些内在的错误，不在产生事件），未来的请求可能失败或者行为异常。

🔗 [**更多: 停掉服务**](/sections/errorhandling/shuttingtheprocess.chinese.md)

<br/><br/>



## ![✔] 2.7 使用一个成熟的日志工具提高错误的可见性

**TL;DR:** 一系列成熟的日志工具，比如Winston，Bunyan和Log4J，会加速错误的发现和理解。忘记console.log吧。

**否则:** 浏览console的log，和不通过查询工具或者一个好的日志查看器，手动浏览繁琐的文本文件，会使你忙于工作到很晚。

🔗 [**更多: 使用好用的日志工具**](/sections/errorhandling/usematurelogger.chinese.md)


<br/><br/>


## ![✔] 2.8 使用你最喜欢的测试框架测试错误流

**TL;DR:** 无论专业的自动化测试或者简单的手动开发测试 - 确保您的代码不仅满足正常的场景，而且处理并且返回正确的错误。测试框架，比如Mocha & Chai可以非常容易的处理这些问题（在"Gist popup"中查看代码实例） 。

**否则:** 没有测试，不管自动还是手动，您不可能依赖代码去返回正确的错误。而没有可以理解的错误，那将毫无错误处理可言。


🔗 [**更多: 测试错误流向**](/sections/errorhandling/testingerrorflows.chinese.md)

<br/><br/>

## ![✔] 2.9 使用APM产品发现错误和宕机时间

**TL;DR:** 监控和性能产品 (别名 APM) 先前一步的检测您的代码库和API，这样他们能自动的，像使用魔法一样的强调错误，宕机和您忽略的性能慢的部分。

**否则:** 您花了很多的力气在测量API的性能和错误，但可能您从来没有意识到真实场景下您最慢的代码块和他们对UX的影响。


🔗 [**更多: 使用APM产品**](/sections/errorhandling/apmproducts.chinese.md)

<br/><br/>


## ![✔] 2.10 捕获未处理的promise rejections

**TL;DR:** 任何在promise中被抛出的异常将被收回和遗弃，除非开发者没有忘记去明确的处理。即使您的代码调用的是process.uncaughtException！解决这个问题可以注册到事件process.unhandledRejection。

**否则:** 您的错误将被回收，无踪迹可循。没有什么可以需要考虑。


🔗 [**更多: 捕获未处理的promise rejection**](/sections/errorhandling/catchunhandledpromiserejection.chinese.md)

<br/><br/>

## ![✔] 2.11 快速查错，验证参数使用一个专门的库

**TL;DR:** 这应该是您的Express最佳实践中的一部分 – assert API输入避免难以理解的漏洞，这类漏洞以后会非常难以追踪。而验证代码通常是一件乏味的事情，除非使用一些非常炫酷的帮助库比如Joi。

**否则:** 考虑这种情况 – 您的功能期望一个数字参数 “Discount” ，然而调用者忘记传值，之后在您的代码中检查是否 Discount!=0 （允许的折扣值大于零），这样它将允许用户使用一个折扣。OMG，多么不爽的一个漏洞。你能明白吗？

🔗 [**更多: 快速查错**](/sections/errorhandling/failfast.chinese.md)

<br/><br/><br/>

<p align="right"><a href="#table-of-contents">⬆ 返回顶部</a></p>

<h1 id="3-code-style-practices"><code>3. 编码风格实践</code></h1>

## ![✔] 3.1 使用ESLint

**TL;DR:** [ESLint](https://eslint.org)是检查可能的代码错误和修复代码样式的事实上的标准，不仅可以识别实际的间距问题, 而且还可以检测严重的反模式代码, 如开发人员在不分类的情况下抛出错误。尽管ESlint可以自动修复代码样式，但其他的工具比如[prettier](https://www.npmjs.com/package/prettier)和[beautify](https://www.npmjs.com/package/js-beautify)在格式化修复上功能强大，可以和Eslint结合起来使用。

**否则:** 开发人员将必须关注单调乏味的间距和线宽问题, 并且时间可能会浪费在过多考虑项目的代码样式。

<br/><br/>

## ![✔] 3.2 Node.js特定的插件

**TL;DR:** 除了仅仅涉及 vanilla JS 的 ESLint 标准规则，添加 Node 相关的插件，比如[eslint-plugin-node](https://www.npmjs.com/package/eslint-plugin-node), [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) and [eslint-plugin-node-security](https://www.npmjs.com/package/eslint-plugin-security)

**否则:** 许多错误的Node.js代码模式可能在检测下逃生。例如，开发人员可能需要某些文件，把一个变量作为路径名 (variableAsPath) ，这会导致攻击者可以执行任何JS脚本。Node.JS linters可以检测这类模式，并及早预警。

<br/><br/>

## ![✔] 3.3 在同一行开始一个代码块的大括号

**TL;DR:** 代码块的第一个大括号应该和声明的起始保持在同一行中。

### 代码示例
```javascript
  // 建议
  function someFunction() {
    // 代码块
  }

  // 避免
  function someFunction()
  {
    // 代码块
  }
```

**否则:** 不遵守这项最佳实践可能导致意外的结果，在Stackoverflow的帖子中可以查看到，如下：

🔗 [**更多:** "Why does a results vary based on curly brace placement?" (Stackoverflow)](https://stackoverflow.com/questions/3641519/why-does-a-results-vary-based-on-curly-brace-placement)

<br/><br/>

## ![✔] 3.4 不要忘记分号

**TL;DR:** 即使没有获得一致的认同，但在每一个表达式后面放置分号还是值得推荐的。这将使您的代码, 对于其他阅读代码的开发者来说，可读性，明确性更强。

**否则:** 在前面的章节里面已经提到，如果表达式的末尾没有添加分号，JavaScript的解释器会在自动添加一个，这可能会导致一些意想不到的结果。

<br/><br/>

## ![✔] 3.5 命名您的方法

**TL;DR:** 命名所有的方法，包含闭包和回调, 避免匿名方法。当剖析一个node应用的时候，这是特别有用的。命名所有的方法将会使您非常容易的理解内存快照中您正在查看的内容。

**否则:** 使用一个核心dump（内存快照）调试线上问题，会是一项非常挑战的事项，因为你注意到的严重内存泄漏问题极有可能产生于匿名的方法。

<br/><br/>

## ![✔] 3.6 变量、常量、函数和类的命名约定

**TL;DR:** 当命名变量和方法的时候，使用 ***lowerCamelCase*** ，当命名类的时候，使用 ***UpperCamelCase*** （首字母大写），对于常量，则 ***UPPERCASE*** 。这将帮助您轻松地区分普通变量/函数和需要实例化的类。使用描述性
