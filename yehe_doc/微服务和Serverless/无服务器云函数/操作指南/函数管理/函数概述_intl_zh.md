云函数是管理、运行的基本单元，通常由一系列配置与一系列可运行代码/软件包组成。

## 函数配置属性
在函数创建时，您需要提供以下信息：
- 函数名 FunctionName：必选，函数名作为函数的唯一标识名称，创建后不可修改。 
- 运行环境 Runtime：必选，指定函数的运行环境，创建后不可修改。
- 函数代码 Code：必选，函数运行的代码，创建后可修改。
- 执行方法 Handler：必选，函数处理方法名称，通常由“文件名.方法名”组成。具体运行环境的情况下稍有不同，可见各 [开发语言说明](https://intl.cloud.tencent.com/document/product/583/11061)。
- 函数描述 Description：可选，可用于记录函数相关作用等信息。


除以上内容外，另外还可通过 [更新函数配置](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/583/19806) 修改以下内容，配置更多函数运行时的信息：
- 内存大小 MemorySize：可选，指定函数运行时可用的内存大小。最小64MB ，最大3072MB。从128MB起，以128MB为阶梯递增，默认128MB。SCF 的 CPU 处理能力与函数配置内存成正比，您可以增加或减少函数配置内存控制分配给函数的配置内存和 CPU 处理能力。
- 运行超时 Timeout：可选，指定函数的最长运行时间，可选值范围为1秒- 900秒，默认3秒。
- 环境变量 Environment：可选，在配置中定义的环境变量可在函数运行时从环境中获取到。
- 私有网络 VPCConfig：可选，配置私有网络后，可将函数置于配置的私有网络中运行。

## 函数可执行的操作
- [创建函数](https://intl.cloud.tencent.com/document/product/583/19806)：创建一个新的函数。
- [更新函数](https://intl.cloud.tencent.com/document/product/583/19806)：
 - 更新函数配置：更新函数的各项配置。
 - 更新函数代码：更新函数的运行代码。
- [获取详情](https://intl.cloud.tencent.com/document/product/583/19809)：获取函数配置、触发器及代码详情。
- [测试运行函数](https://intl.cloud.tencent.com/document/product/583/14572)：根据需要，通过同步或异步方法触发函数运行。
- [获取日志](https://intl.cloud.tencent.com/document/product/583/19810)：获取函数运行情况及输出的日志。
- [删除函数](https://intl.cloud.tencent.com/document/product/583/19807)：删除不再需要的函数。

函数的触发器相关操作有：
- [创建触发器](https://intl.cloud.tencent.com/document/product/583/31441)：创建一个新的触发器。
- [删除触发器](https://intl.cloud.tencent.com/document/product/583/31442)：删除已有触发器。

## 执行方法
执行方法表明了调用云函数时需要从哪个文件中的哪个函数开始执行，可分为以下三种方式：
- 一段式格式为**"[文件名]"**，支持 Golang 环境时使用，例如 "main"。
- 两段式格式为**"[文件名].[函数名]"**，支持 Python、Node.js 及 PHP 环境时使用，例如 "index.main_handler"。
>?两段式的执行方法中，前一段指向代码包中不包含后缀的文件名，后一段指向文件中的入口函数名。需确保代码包中的文件名后缀与语言环境匹配，例如 Python 环境为 `.py` 文件，Node.js 环境为 `.js` 文件。 
>
- 三段式格式为 **"[package].[class]::[method]"**，支持 Java 环境时使用，例如 "example.Hello::mainHandler"。

