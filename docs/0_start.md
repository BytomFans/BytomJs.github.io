---
id: start
title: quick start
sidebar_label: SDK环境配置
---
## 下载bytom-js-sdk

注意：所有教程默认你已经安装了node.js、npm的开发环境，以下我们提供两种方法来部署bytom-js-sdk到你的项目上。

### 使用npm安装依赖包

1.在项目根目录创建`package.json`文件，运行：

```bash
npm init
```

2.初始化好之后，下载bytom-sdk依赖包。

```bash
npm install bytom-sdk
```

3.我们可以引入bytom-sdk模块，并通过实例化来创建处理程序。

```js
var require = require('bytom-sdk')
```

### 使用Git安装

将通过两种方法介绍
直接从git上clone该项目：<https://github.com/Bytom/bytom-node-sdk>

```bash
git clone https://github.com/lxlxw/bytom-php-sdk.git
```

## 使用实例

下面是一个如何使用SDK来发送消息的例子：

```js
//引入bytom-sdk模块
const bytom = require('bytom-sdk')
const url = 'http://localhost:9888'

// 当远程调试时，accessToken是不能为空的，本例子默认在本地调试运行
// 连接上比原链节点
const accessToken = ''

//实例化一个bytom对象
const client = new bytom.Client(url, accessToken)

//触发创建key事件
const keyPromise = client.keys.create({ 
    alias:'alice', 
    password: '123456'
   })
```

返回：

```json
{
  "alias": "alice",
  "xpub": "a7dae957c2d35b42efe7e6871cf5a75ebd2a0d0e51caffe767db42d3e6d69dbe211d1ca492ecf05908fe6fa625ad61b3253375ea744c9442dd5551613ba50aea",
  "file": "/Path/To/Library/Bytom/keystore/UTC--2018-04-22T06-30-27.609315219Z--0e34293c-8856-4f5f-b934-37456a3820fa"
}
```

## 其他示例

请参考文档：[API中文文档](http://localhost:3000/docs/key)

## 支持和反馈

如果你发现了该SDK的bug，请直接在github上提交issue： [bytom-node-sdk Issues](https://github.com/Bytom/bytom-node-sdk/issues)

## 联系

- 邮箱：[x@xwlin.com](mailto:x@xwlin.com)


