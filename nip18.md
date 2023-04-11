---
description: 原文：https://github.com/nostr-protocol/nips/blob/master/18.md
---

NIP-18
======

快转提升
-------

`draft` `optional` `author:jb55` `author:fiatjaf` `author:arthurfranca`

快转提升是一种 `kind 6` 的脑特记录，用来给其粉丝提示某另外一个事件很值得读。

快转提升事件的 `content` 为空。可选地，它可能包含已转发笔记事件的字符串化 JSON 对象，以便快速查找。

快转提升事件必须包括一个带有被转发笔记`id`的`e`标签。该标签必须在其第三项中包含继电器URL，以指示可以从哪里获取它。

快转提升应该包括一个具有被转发事件的`pubkey` 的 `p`标签。

## 引用转发

引用转发本质就是一种 `kind 1` 事件，只是具有嵌入的`e`标签（参见 [NIP-08](nip08.md) 和 [NIP-27](nip27.md)）。
因为引用转发包含了`e`标签，所以它可能会在回复被转发笔记时出现。
