---
id: mining
title: Mining API
sidebar_label: Bytom.Mining.API
---

## is-mining

返回挖矿状态。

#### 参数

none

#### 返回


- `Boolean` - *is_mining*, 节点是否启动了挖矿.

#### 例子
```js
const keyPromise = client.status.isMining()
var sync = keyPromise.then((res) => console.log(res)) 
```
```js
$node test.js
//response
{
  "is_mining": true
}
```

## set-mining

启动节点。

#### 参数

- `Boolean` - *is_mining*, 节点是否启动了挖矿.

#### 例子
```js
const keyPromise = client.status.setMining({
    is_mining: true
})
var sync = keyPromise.then((res) => console.log(res)) 
```
```js
$node test.js
//response
//none
```