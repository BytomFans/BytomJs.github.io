---
id: block
title: Block API
sidebar_label: Bytom.Block.API
---

## get-block-count

返回当前区块链的高度.

#### 参数

none

#### 返回

- `Integer` - *block_count*, 当前的区块高度.

#### 例子
```js
const keyPromise = client.block.getBlockCount()
var sync = keyPromise.then((res) => console.log(res)) 
```
```js
$ node test.js
//response
{ block_count: 217520 }
```

## get-block-hash

返回当前区块的hash.

#### 参数

none

#### 返回

- `String` - *block_hash*, 最近的区块hash.

#### 例子
```js
const keyPromise = client.block.getBlockHash()
var sync = keyPromise.then((res) => console.log(res)) 
```
```js
$ node test.js
//response
$ node test.js
{ 
    block_hash:'c4f5e0214f5f46f2de4022dfca4976c4c4d0078eb0f434f83ffdd8999648e4df' 
}
```

## get-block

区块高度或块哈希返回详细信息块。

#### 参数

`Object`: block_height | block_hash

可选:

- `String` - *block_hash*, 区块hash.
- `Integer` - *block_height*, 区块高度.

#### 返回

`Object`:

- `String` - *hash*, 区块hash.

- `Integer` - *size*, 区块大小.

- `Integer` - *version*, 区块版本.

- `Integer` - *height*, 区块高度.

- `String` - *previous_block_hash*, 前一个区块hash.

- `Integer` - *timestamp*, 区块时间戳.

- `Integer` - *nonce*, 随机数值.

- `Integer` - *bits*, 区块难度.

- `String` - *difficulty*, 难度值(String type).

- `String` - *transaction_merkle_root*, 交易的默克尔根.

- `String` - *transaction_status_hash*, 交易状态的默克尔根.

- `Array of Object`- * transactions*, 交易对象:

  - `String` - *id*, transaction id, 交易hash.

  - `Integer` - *version*, 交易版本.

  - `Integer` - *size*, 交易大小.

  - `Integer` - *time_range*, 响应请求时的unix时间戳.

  - `Boolean` - *status_fail*, 请求状态是否是失败的.

  - `String` - *mux_id*, 前一笔交易的mux id(utxo的源ID).

  - `Array of Object`- *inputs*, 交易对象的输入.

    - `String` - *type*, 输入操作的类型，可用选项包括: 'spend', 'issue', 'coinbase'.
    - `String` - *asset_id*, 资产id.
    - `String` - *asset_alias*, 资产名字.
    - `Object` - *asset_definition*, 资产定义(json 对象).
    - `Integer` - *amount*, 资产数量.
    - `Object` - *issuance_program*, issuance program, 当交易类型为'issue'.
    - `Object` - *control_program*, control program of account, 当交易类型为'spend'.
    - `String` - *address*, 账户地址, 当类型是'spend'时存在.
    - `String` - *spent_output_id*, the front of outputID to be spent in this input, 当交易类型为'spend'.
    - `String` - *account_id*, 账户id.
    - `String` - *account_alias*, 账户名字.
    - `Object` - *arbitrary*, 任意信息都可以由矿工设置，当交易类型为'coinbase'时.

  - `Array of Object` - *outputs* , 交易输出对象.

    - `String` - *type*, 输出action的类型，可选项包括:"retire","control".
    - `String` - *id*, 与utxo相关的交易输出id.
    - `Integer` - *position*, 输出的位置.
    - `String` - *asset_id*, 资产id.
    - `String` - *asset_alias*, 资产名字.
    - `Object` - *asset_definition*, 资产定义(json 对象).
    - `Integer` - *amount*, 资产数量.
    - `String` - *account_id*, 账户id.
    - `String` - *account_alias*, 账户名字.
    - `Object` - *control_program*, 账户的控制程序.
    - `String` - *address*, 账户地址.

#### 例子

通过block_hash或block_height获取指定的块信息，如果两者都存在，则块结果通过哈希查询。
```js
const keyPromise = client.block.getBlock({
    block_height: 217521, 
    block_hash: 'c4f5e0214f5f46f2de4022dfca4976c4c4d0078eb0f434f83ffdd8999648e4df'
})
var sync = keyPromise.then((res) => console.log(res)) 
```
```js
$ node test.js
//response
{ 
  hash:'c4f5e0214f5f46f2de4022dfca4976c4c4d0078eb0f434f83ffdd8999648e4df',
  size: 416,
  version: 1,
  height: 217521,
  previous_block_hash:
   '36b6b386ab8a0d31e50f63cd4cc7d1a856c37772e199b4490c58939ceb66d9cf',
  timestamp: 1555574169,
  nonce: 936937894344669600,
  bits: 2017612633064242700,
  difficulty: '31878122073',
  transaction_merkle_root:
   '47091250d24330e5b7d5964579600accd792821ae9051a8d10dffe5cc693c290',
  transaction_status_hash:
   'c9c377e5192668bc0a367e4a4764f11e7c725ecced1d7b6a492974fab1b6d5bc',
  transactions:
   [ { id:
        'cc074284c301a97d0c73f1c3081768b9b0ce1e872c99a0c497ef632dc7a47646',
       version: 1,
       size: 82,
       time_range: 0,
       inputs: [Array],
       outputs: [Array],
       status_fail: false,
       mux_id:
        '001f63a7e82991a574c5bdcd09f8cac4a75cd100b3d4b82cb2d87341df66e3b8' } ] 
}
```

## get-block-header

按块高度或块哈希返回详细信息块标头。

#### 参数

`Object`: block_height | block_hash

可选:

- `String` - *block_hash*, 区块hash.
- `Integer` - *block_height*, 区块高度.

#### 返回

- `Object` - *block_header*, 区块头.
- `Integer` - *reward*, 区块奖励.

#### 例子
```js
const keyPromise = client.block.getBlockHeader({
    block_height: 217521, 
    block_hash: 'c4f5e0214f5f46f2de4022dfca4976c4c4d0078eb0f434f83ffdd8999648e4df'
})
var sync = keyPromise.then((res) => console.log(res)) 
```
```js
$ node test.js
//response
{
    block_header:
   '0101b1a30d36b6b386ab8a0d31e50f63cd4cc7d1a856c37772e199b4490c58939ceb66d9cf99
dbe0e5054047091250d24330e5b7d5964579600accd792821ae9051a8d10dffe5cc693c290c9c377
e5192668bc0a367e4a4764f11e7c725ecced1d7b6a492974fab1b6d5bc85f39088d081ab800db9fb
8981808080801c',
  reward: 41250000000 
}

```

## get-difficulty

通过块高度或块散列返回块高度，当请求为空时返回当前块高度。

#### 参数

- `String` - *block_hash*, 区块hash.
- `Integer` - *block_height*, 区块高度.

#### 返回

- `Integer` - *bits*, 区块的位.
- `String` - *difficulty*, 区块难度.
- `String` - *hash*, 区块hash.
- `Integer` - *height*, 区块高度.

##### 例子

为当前块或指定的块散列/高度获取困难。
```js
const keyPromise = client.block.getDifficulty({
    block_height: 217521, 
    block_hash: 'c4f5e0214f5f46f2de4022dfca4976c4c4d0078eb0f434f83ffdd8999648e4df'
})
var sync = keyPromise.then((res) => console.log(res)) 
```
```js
$ node test.js
//response
{ 
   hash:
   'c4f5e0214f5f46f2de4022dfca4976c4c4d0078eb0f434f83ffdd8999648e4df',
  height: 217521,
  bits: 2017612633064242700,
  difficulty: '31878122073' 
}
```

## get-hash-rate

通过块高度或块散列返回块散列率，当请求为空时，它返回当前块散列率。

#### 参数

- `String` - *block_hash*, 区块hash.
- `Integer` - *block_height*, 区块高度.

#### 返回

- `Integer` - *hash_rate*, 区块的出块难度.
- `String` - *hash*, 区块 hash.
- `Integer` - *height*, 区块 height.

#### 例子

获取当前块或指定块散列/高度的哈希率。
```js
const keyPromise = client.block.getHashRate({
    block_height: 217521, 
    block_hash: 'c4f5e0214f5f46f2de4022dfca4976c4c4d0078eb0f434f83ffdd8999648e4df'
})
var sync = keyPromise.then((res) => console.log(res)) 
```
```js
$ node test.js
//response
{ 
  hash:
   'c4f5e0214f5f46f2de4022dfca4976c4c4d0078eb0f434f83ffdd8999648e4df',
  height: 217521,
  hash_rate: 203045363 
}


```

