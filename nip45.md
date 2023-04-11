---
description: 原文：https://github.com/nostr-protocol/nips/blob/master/45.md
---

NIP-45
======

事件计数
--------------

`draft` `optional` `author:staab`

中继们可以支持 `COUNT` 动词，该动词提供了获取事件计数的机制。

## 动机

客户端可能希望对连接的中继执行的一些查询非常昂贵，例如，为了检索给定公钥的跟随者计数，客户端必须查询引用给定公钥的所有3类事件并对其进行计数。作为替代方案，结果可以由客户端或单独的索引服务器缓存，但这两种选择都会通过在Nostr之上创建第二层协议来削弱网络的分散性。

## 过滤器和返回值

此NIP定义了一个名为`COUNT`的谓词，该谓词接受中指定的订阅id和筛选器 [NIP 01](nip01.md).

计数是使用`{count: <integer>}`形式的`COUNT`响应返回的。中继可以使用概率计数来减少计算需求。

例如:

```
# Followers count
["COUNT", "", {kinds: [3], '#p': [<pubkey>]}]
["COUNT", "", {count: 238}]

# Count posts and reactions
["COUNT", "", {kinds: [1, 7], authors: [<pubkey>]}]
["COUNT", "", {count: 5}]
```
