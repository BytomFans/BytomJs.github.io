---
id: key
title: Key API
sidebar_label: Bytom.Key.API
---

## create-key

本质上是创建私钥，返回密钥的信息，其中私钥保存在本地文件中，加密对用户不可见。

#### 参数

- `String` - *alias* ，密钥的名字
- `String` - *password* ，私钥的密码

#### 返回

- `String` - *alias* , 密钥的名字

- `String` - *xpub* , 公钥

- `String` - *file* , 私钥文件在本地的存放路径
#### 例子
```js
const client = new bytom.Client(url, accessToken)
const keyPromise = client.keys.create({ 
    alias:'alice', 
    password: '123456'
   })
var sync = keyPromise.then((res) => console.log(res)) 
```
```json
$ node test.js
//response
[
  {
      "alias": "alice",
      "xpub": "a7dae957c2d35b42efe7e6871cf5a75ebd2a0d0e51caffe767db42d3e6d69dbe211d1ca492ecf05908fe6fa625ad61b3253375ea744c9442dd5551613ba50aea",
      "file": "/Path/To/Library/Bytom/keystore/UTC--2018-04-22T06-30-27.609315219Z--0e34293c-8856-4f5f-b934-37456a3820fa"
  }
]
```
## list-keys

返回所有可用的密钥列表。

#### 参数

none

#### 返回

- `Array of Object` , 客户端所拥有的所有私钥信息
  - `object` :
    - `String`  - *alias* , 私钥的名字
    - `String` - *xpub*, 公钥
#### 例子
```js
const client = new bytom.Client(url, accessToken)
var con = client.accounts.listAll();
var sync = con.then((res) => console.log(res)) 
```
```json
$ node test.js
//response
[
  {
    "alias": "alice",
    "xpub": "a7dae957c2d35b42efe7e6871cf5a75ebd2a0d0e51caffe767db42d3e6d69dbe211d1ca492ecf05908fe6fa625ad61b3253375ea744c9442dd5551613ba50aea",
    "file": "/Path/To/Library/Bytom/keystore/UTC--2018-04-21T02-35-15.035935116Z--4f2b8bd7-0576-4b82-8941-6cc6da05efe3"
  },
  {
    "alias": "bob",
    "xpub": "d30a810e88532f73816b7b5007d413cbd21e526ae9159023e5262511893adc1526b8eacd691b27c080201d7d79336a4f3d2cb4c167d997821cad445765916254",
    "file": "/Path/To/Library/Bytom/keystore/UTC--2018-04-22T06-30-27.609315219Z--0e34293c-8856-4f5f-b934-37456a3820fa"
  }
]
```

## delete-key
删除现有的密钥，请确保相关账户中没有余额。
#### 参数
- `String` - *xpub*, 公钥
- `String` - *password*,密钥的密码
#### 返回
如果删除成功则返回none
#### 例子
```js
const keyPromise = client.keys.delete({          xpub:'a7dae957c2d35b42efe7e6871cf5a75ebd2a0d0e51caffe767db42d3e6d69dbe211d1ca492ecf05908fe6fa625ad61b3253375ea744c9442dd5551613ba50aea', 
    password: '123456'
   })
var sync = keyPromise.then((res) => console.log(res)) 
```
```json
$ node test.js
//response
// none
```
##  reset-key-password

重置密钥密码。

#### 参数

- `String` - *xpub* , 公钥
- `String` - *old_password*, 密钥文件的旧密码
- `String` - *new_password* , 密钥文件的新密码

#### 返回

- `Boolean` - *changed* ,判断重置密钥密码后的状态，若为success则返回true

#### 例子
```js
const keyPromise = client.keys.resetPassword({ 
 xpub:'6add0a90da032fe9d13b006cc0161130f905cd9fe5539744eeedf09e5ccf263b362d6acbdff50751cd6ba7176093ba6a8e90e4ed3a3427a5d13973da749847b6', 
    oldPassword: '123456',
    newPassword:'234567'
   })
var sync = keyPromise.then((res) => console.log(res)) 
```
```json
$ node test.js
//response
{ changed: true }
```