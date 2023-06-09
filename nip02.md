---
description: 原文：https://github.com/nostr-protocol/nips/blob/master/02.md
---

# NIP02

## 联系人列表和昵称

`final` `optional` `author:fiatjaf` `author:arcbtc`

具有 KIND `3` 的特殊事件，即"联系人列表"，被定义为具有标签列表 `p`，每个标签对应于一个正在跟随的/已知的配置文件。

每个标签条目都应包含配置文件的键、可以找到来自该键的事件的中继 URL（如果不需要，可以设置为空字符串），以及该配置文件的本地名称（或" petname "）（也可以设置为空字符串或不提供），即 `["p", <32-bytes hex key>, <main relay URL>, <petname>]`。这 `content` 可以是任何东西，应该被忽略。

例如：

```json
{
  "kind": 3,
  "tags": [
    ["p", "91cf9..4e5ca", "wss://alicerelay.com/", "alice"],
    ["p", "14aeb..8dad4", "wss://bobrelay.com/nostr", "bob"],
    ["p", "612ae..e610f", "ws://carolrelay.com/ws", "carol"]
  ],
  "content": "",
  ...other fields
}
```

发布的每个新联系人列表都会覆盖过去的联系人列表，因此它应该包含所有条目。中继和客户端应在收到新的联系人列表后立即删除过去的联系人列表。

## 用途

### 联系人列表备份

如果有人认为中继会将其事件存储足够长的时间，则可以使用此 Kind-3 事件来备份其以下列表，并在不同的设备上恢复。

### 配置文件发现和上下文增强

客户端可以依靠 Kind-3 事件来显示正在浏览的简档所跟随的人的列表；根据可能关注或浏览的其他人的联系人列表，列出要关注的人的建议列表；或者在其他上下文中显示数据。

### 中继共享

客户可以为其每个联系人发布具有良好中继的联系人的完整列表，以便其他客户可以在需要时使用这些列表来更新其内部中继列表，从而增加审查阻力。

### 宠物名称方案

客户端可以使用这些联系人列表中的数据来构造从其他人的联系人列表派生的本地表["petname"](http://www.skyhunter.com/marcs/petnames/IntroPetNames.html)。这减少了对人类可读的全局名称的需求。例如：

用户有一个内部联系人列表，上面写着

```json
[
  ["p", "21df6d143fb96c2ec9d63726bf9edc71", "", "erin"]
]
```

并收到两个联系人列表，其中一个 `21df6d143fb96c2ec9d63726bf9edc71` 列表显示

```json
[
  ["p", "a8bb3d884d5d90b413d9891fe4c4e46d", "", "david"]
]
```

另一个 `a8bb3d884d5d90b413d9891fe4c4e46d` 说

```json
[
  ["p", "f57f54057d2a7af0efecc8b0b66f5708", "", "frank"]
]
```

当用户看到 `21df6d143fb96c2ec9d63726bf9edc71` 客户端时，可以改为显示erin；当用户看到 `a8bb3d884d5d90b413d9891fe4c4e46d` 客户端时，可以改为显示david.erin；当用户看到 `f57f54057d2a7af0efecc8b0b66f5708` 时，客户端可以改为显示frank.david.erin。
