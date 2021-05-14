# Apifox 介绍

[Apifox 官网：apifox.cn](https://www.apifox.cn/)

> 软件开发过程中，接口管理、调试、自动化测试是必不可少的，我们经常使用 Postman 等工具来进行接口调试，在接口调试方面 Postman 做的非常出色。但是在整个软件开发过程中，接口调试只是其中的一部分，还有很多事情 Postman 无法完成，或者`无法高效完成`，比如：接口文档定义、Mock 数据、接口自动化测试等等。而 Apifox 就是为此而生的。

## 接口管理现状

### 一、常用解决方案

1. 使用 Swagger 管理接口文档
1. 使用 Postman 调试接口
1. 使用 RAP Mock 数据
1. 使用 JMeter 做接口自动化测试

### 二、存在的问题

维护不同工具之间数据一致性非常困难、非常低效。并且这里不仅仅是工作量的问题，更大的问题是多个系统之间数据不一致，导致协作低效，频繁出问题，开发人员痛苦不堪。

1. 开发人员在 Swagger 定义好文档后，接口调试的时候还需要去 Postman 再定义一遍。
2. 前端开发 Mock 数据的时候又要去 RAP 定义一遍，手动设置好 Mock 规则。
3. 测试人员需要去 JMeter 定义一遍。
4. 前端根据 RAP Mock 出来的数据开发完，后端根据 Swagger 定义的接口文档开发完，各自测试测试通过了，本以为可以马上上线，结果一对接发现各种问题：原来开发过程中接口变更，只修改了 Swagger，但是没有及时同步修改 RAP。
5. 同样，测试在 JMeter 写好的测试用例，真正运行的时候也会发现各种不一致。
6. 时间久了，各种不一致会越来越严重。

## Apifox 解决方案

### 一、如何解决这些问题

#### 1、Apifox 定位

`Apifox = Postman + Swagger + Mock + JMeter`

通过一套系统、一份数据，解决多个系统之间的数据同步问题。只要定义好接口文档，接口调试、数据 Mock、接口测试就可以直接使用，无需再次定义；接口文档和接口开发调试使用同一个工具，接口调试完成后即可保证和接口文档定义完全一致。高效、及时、准确！

#### 2、Apifox  功能

1. 接口文档定义：Apifox 遵循 [OpenApi](https://www.openapis.org/) 3.0 (原Swagger)、[JSON Schema](https://json-schema.org/) 规范的同时，提供了非常好用的可视化文档管理功能，零学习成本，非常高效。
2. 接口调试：Postman 有的功能，比如环境变量、预执行脚本、后执行脚本、Cookie/Session 全局共享 等功能，Apifox 都有，并且和 Postman 一样高效好用。
3. 数据 Mock：内置 [Mock.js](http://mockjs.com/) 规则引擎，非常方便 mock 出各种数据，并且可以在定义数据结构的同时写好 mock 规则。支持添加“期望”，灵活配置根据参数值返回不同数据内容。最重要的是 Apifox `零配置` 即可 Mock 出非常人性化的数据，具体在本文后面介绍。
4. 接口自动化测试：提供接口集合测试，可以通过选择接口（或接口用例）快速创建测试集。目前接口自动化测试更多功能还在开发中，敬请期待！目标是： JMeter 有的功能基本都会有，并且要更好用。

### 二、Apifox 做的不仅仅是数据打通

如果你认为 Apifox 只做了数据打通，来提升研发团队的效率，那就错了。Apifox 还做了非常多的创新，来提升开发人员的效率。

#### 1、调试时自动校验数据结构

使用 Apifox 调试接口的时候，系统会根据接口文档里的定义，自动校验返回的数据结构是否正确，无需通过肉识别，也无需手动写断言脚本检测，非常高效！

![Apifox 自动校验数据结构](http://cdn.apifox.cn/www/docs/api-case/auto-validation-schema.jpg)

#### 2、数据模型定义、引用

可以独立定义数据模型，接口定义时可以直接引用数据模型，数据模型之间也可以相互引用。同样的数据结构，只需要定义一次即可多处使用；修改的时候只需要修改一处，多处实时更新，避免不一致。

#### 3、接口用例管理

通常一个接口会有多种情况用例，比如 `正确用例` `参数错误用例` `数据为空用例` `不同数据状态用例`。定义接口的时候定义好这些不同状态的用例，接口调试的时候直接运行，非常高效。

#### 4、零配置 Mock 出非常人性化的数据

先放一张图对比下 Apifox 和其他同类工具 `零配置` mock 出来的数据效果：

![Apifox Mock 数据结果对比同类工具](http://cdn.apifox.cn/www/docs/mock/mock-result-compare.jpg)

可以看出 Apifox `零配置` Mock 出来的数据和真实情况是非常接近的，前端开发可以直接使用，而无需再手动写mock规则。

Apifox 如何做到高效率、零配置生成非常人性化的 mock 数据：

1. Apifox 根据接口定义里的数据结构、数据类型，自动生成 mock 规则。
2. Apifox 内置智能 mock 规则库，根据字段名、字段数据类型，智能优化自动生成的 mock 规则。如：名称包含字符串`image`的`string`类型字段，自动 mock 出一个图片地址 URL；包含字符串`time`的`string`类型字段，自动 mock 出一个时间字符串；包含字符串`city`的`string`类型字段，自动 mock 出一个城市名。
3. Apifox 根据内置规则，可自动识别出图片、头像、用户名、手机号、网址、日期、时间、时间戳、邮箱、省份、城市、地址、IP等字段，从而 Mock 出非常人性化的数据。
4. 除了内置 mock 规则，用户还可以自定义规则库，满足各种个性化需求。支持使用 `正则表达式`、`通配符` 来匹配字段名自定义 mock 规则。

#### 5、代码自动生成

根据接口模型定义，自动生成各种语言/框架（如 TypeScript、Java、Go、Swift、ObjectiveC、Kotlin、Dart、C++、C#、Rust 等）的业务代码（如 Model、Controller、单元测试代码等）和接口请求代码。目前 Apifox 支持 130 种语言及框架的代码自动生成。

更重要的是：你可以通过`自定义代码模板`来生成符合自己团队的架构规范的代码，满足各种个性化的需求。

#### 6、导入、导出

1. 支持导出 `OpenApi (原Swagger)`、`Markdown`、`Html` 等数据格式，因为可以导出`OpenApi`格式数据，所以你可以利用 OpenApi (Swagger) 丰富的生态工具完成各种接口相关的事情。
2. 支持导入 `OpenApi (原Swagger)`、`Postman`、`HAR`、`RAML`、`RAP2`、`YApi`、`Eolinker`、`DOClever`、`ApiPost` 、`Apizza` 、`API Blueprint`、`I/O Docs`、`WADL`、`Google Discovery `等数据格式，方便旧项目迁移。

### 三、更多 Apifox 功能截图

![接口调试](http://cdn.apifox.cn/www/screenshot/frame-apifox-api-case-1.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-api-case-2.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-api-definition-1.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-schema-1.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-api-definition-2.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-api-definition-3.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-test-suite-1.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-test-suite-2.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-test-suite-3.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-mock-1.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-mock-2.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-mock-3.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-codegen-1.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-codegen-2.png)

![](http://cdn.apifox.cn/www/screenshot/frame-apifox-setting-import-1.png)

![Apifox 多种主题色可选](http://cdn.apifox.cn/www/screenshot/light-frame-apifox-theme-1.png)



### 四、 Apifox 下载地址

请访问 Apifox 官网下载：[https://www.apifox.cn/](https://www.apifox.cn/)

