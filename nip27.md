---
description: 原文：https://github.com/nostr-protocol/nips/blob/master/27.md
---

NIP-27
======

文本注释参考
--------------------

`draft` `optional` `author:arthurfranca` `author:hodlbod` `author:fiatjaf`

本文档标准化了客户端对`.content`中具有可读文本的任何事件（如kinds 1和30023）的`.content`内的其他事件和配置文件的内联引用的处理。

创建事件时，客户端应使用[NIP-21](nip21.md)代码在`.content`中间包含对其他配置文件和其他事件的提及，例如`nostr:nprofile1qqsw3dy8cpu...6x2argwghx6egsqstvg`。

为每个引用包含[NIP-10]](nip10.md)-样式标记（`["e", <hex-id>, <relay-url>, <marker>]`）是可选的，客户端应该在希望被提及的配置文件被通知被提及时，或者当他们希望被引用的事件将其提及识别为答复时，都这样做。

接收到带有`nostr:...`的事件的读取器客户端在其`.content`中的提及可以在该过程中进行任何所需的上下文增强（例如，链接到配置文件或显示所提及事件内容的预览）。如果将这些提及转化为链接，它们可能会成为内部链接[NIP-21](nip21.md)链接或指向将处理这些引用的网络客户端的直接链接。

---

## 个人资料提及过程示例

假设Bob正在客户端中编写注释，该客户端具有用户的搜索和自动完成功能，当用户写入字符`@`时会触发该功能。

当Bob键入`"hello @mat"`时，客户端将提示他自动完成[mattn's profile](https://iris.to/d34110060782337c8864ff76321a821f2dbbcfb0bb33864b1cc48712abd84a80)，显示图片和名称。

Bob按下“回车”，现在他看到他键入的Note是`"hello @mattn"`，`@mattn`突出高亮蓝紫色显示，表明这是一个提及。然而，在内部，事件看起来是这样的：

```json
{
  "content": "hello nostr:nprofile1qqszclxx9f5haga8sfjjrulaxncvkfekj097t6f3pu65f86rvg49ehqj6f9dh",
  "created_at": 1679790774,
  "id": "f39e9b451a73d62abc5016cffdd294b1a904e2f34536a208874fe5e22bbd47cf",
  "kind": 1,
  "pubkey": "79be667ef9dcbbac55a06295ce870b07029bfcdb2dce28d959f2815b16f81798",
  "sig": "f8c8bab1b90cc3d2ae1ad999e6af8af449ad8bb4edf64807386493163e29162b5852a796a8f474d6b1001cddbaac0de4392838574f5366f03cc94cf5dfb43f4d",
  "tags": [
    [
      "p",
      "2c7cc62a697ea3a7826521f3fd34f0cb273693cbe5e9310f35449f43622a5cdc"
    ]
  ]
}
```

（或者，提到的可能是一个`nostr:npub1...` URL）

在Bob发布此事件并且Carol看到它之后，她的客户端最初将按原样显示`.content`，但稍后它将解析`.content`，并查看其中是否有`nostr:` URL，对其进行解码，从中提取公钥（并可能中继提示），从其内部数据库或中继中获取该配置文件，然后将完整的URL替换为名称`@mattn`，带有指向该配置文件的内部页面视图的链接。

## 详细且可能不必要的考虑因素

- 上面的例子非常具体，但这并不意味着所有客户端都必须实现相同的流。可能有一些客户端根本不支持自动完成，所以它们只允许用户将原始[NPI-19](nip19.md)代码粘贴到文本主体中，然后在发布事件之前在这些代码前面加上`nostr:`。
- 引用其他事件的流程是类似的：用户可以粘贴`note1...`或`nevent1...`代码，客户端会将其转换为`nostr:note1...` 或`nostr:nevent1...` URL。然后，在阅读这些参考资料后，客户可能会在预览框或类似的东西中显示参考的笔记——或者什么都不显示。
- 可以采用其他显示过程：例如，如果设计用于仅处理`kind:1`文本注释的客户端在`.content`中看到例如[`kind:30023`](nip23.md) `nost:naddr1…`URL引用，则它可以决定将其转换为能够显示此类事件的某些硬编码Web应用程序的链接。
- 客户端可以为用户提供包括或不包括上述事件或配置文件的标签的选项。如果有人想在不通知他们的情况下提及`mattn`，但在他们的笔记中仍然有一个很好的可扩展/可点击的个人资料链接，他们可以指示客户不为该特定提及创建一个`["p", ...]` 标签。
- 同样，如果有人想引用另一条注释，但他们的引用并不意味着与对同一条注释的其他回复一起出现，他们的客户可以选择不在`.content`内的任何给定`nost:nevent1…`URL中包含相应的`["e", ...]`标记。客户可能会决定向用户展示这些高级功能，或者对事情更加固执己见。
