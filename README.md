# NIPs 汉化版本

From [https://github.com/nostr-protocol/nips](https://github.com/nostr-protocol/nips/)

NIPs stand for **Nostr Implementation Possibilities**. They exist to document what may be implemented by [Nostr](https://github.com/fiatjaf/nostr)-compatible _relay_ and _client_ software.

- [NIP-01: Basic protocol flow description](nip01.md)
- [NIP-02: Contact List and Petnames](nip02.md)
- [NIP-03: OpenTimestamps Attestations for Events](nip03.md)
- [NIP-04: Encrypted Direct Message](nip04.md)
- [NIP-05: Mapping Nostr keys to DNS-based internet identifiers](nip05.md)
- [NIP-06: Basic key derivation from mnemonic seed phrase](nip06.md)
- [NIP-07: `window.nostr` capability for web browsers](nip07.md)
- [NIP-08: Handling Mentions](nip08.md) – `unrecommended`: deprecated in favor of [NIP-27](nip27.md)
- [NIP-09: Event Deletion](nip09.md)
- [NIP-10: Conventions for clients' use of `e` and `p` tags in text events](nip10.md)
- [NIP-11: Relay Information Document](nip11.md)
- [NIP-12: Generic Tag Queries](nip12.md)
- [NIP-13: Proof of Work](nip13.md)
- [NIP-14: Subject tag in text events.](14.md)
- [NIP-16: Event Treatment](nip16.md)
- [NIP-18: Reposts](nip18.md)
- [NIP-19: bech32-encoded entities](nip19.md)
- [NIP-20: Command Results](nip20.md)
- [NIP-21: `nostr:` URL scheme](nip21.md)
- [NIP-22: Event `created_at` Limits](nip22.md)
- [NIP-23: Long-form Content](nip23.md)
- [NIP-25: Reactions](nip25.md)
- [NIP-26: Delegated Event Signing](nip26.md)
- [NIP-27: Text Note References](nip27.md)
- [NIP-28: Public Chat](nip28.md)
- [NIP-33: Parameterized Replaceable Events](nip33.md)
- [NIP-36: Sensitive Content](nip36.md)
- [NIP-39: External Identities in Profiles](nip39.md)
- [NIP-40: Expiration Timestamp](nip40.md)
- [NIP-42: Authentication of clients to relays](nip42.md)
- [NIP-45: Counting results](nip45.md)
- [NIP-46: Nostr Connect](nip46.md)
- [NIP-50: Keywords filter](nip50.md)
- [NIP-51: Lists](nip51.md)
- [NIP-56: Reporting](nip56.md)
- [NIP-57: Lightning Zaps](nip57.md)
- [NIP-58: Badges](nip58.md)
- [NIP-65: Relay List Metadata](nip65.md)
- [NIP-69: Zap Vote](nip69.md)
- [NIP-78: Application-specific data](nip78.md)

## Event Kinds

| kind          | 描述description                  | NIP           |
| ------------- | -------------------------------- | ------------- |
| 0             | 资料Metadata                     | [1](nip01.md)  |
| 1             | 短文Short Text Note              | [1](nip01.md)  |
| 2             | 推荐中继Recommend Relay          | [1](nip01.md)  |
| 3             | 关注列表Contacts                 | [2](nip02.md)  |
| 4             | 私聊Encrypted Direct Messages    | [4](nip04.md)  |
| 5             | 撤销Event Deletion               | [9](nip09.md)  |
| 6             | 快转提升Reposts                  | [18](nip18.md) |
| 7             | 点赞Reaction                     | [25](nip25.md) |
| 8             | 徽章授予Badge Award              | [58](nip58.md) |
| 40            | Channel Creation                 | [28](nip28.md) |
| 41            | Channel Metadata                 | [28](nip28.md) |
| 42            | Channel Message                  | [28](nip28.md) |
| 43            | Channel Hide Message             | [28](nip28.md) |
| 44            | Channel Mute User                | [28](nip28.md) |
| 1984          | 举报Reporting                    | [56](nip56.md) |
| 6969          | 投票Zap Vote                     | [69](nip69.md) |
| 9734          | Zap Request                      | [57](nip57.md) |
| 9735          | 打赏Zap                          | [57](nip57.md) |
| 10000         | 沉默Mute List                    | [51](nip51.md) |
| 10001         | 固定Pin List                     | [51](nip51.md) |
| 10002         | 中继列表Relay List Metadata      | [65](nip65.md) |
| 22242         | Client Authentication            | [42](nip42.md) |
| 24133         | Nostr Connect                    | [46](nip46.md) |
| 30000         | 人群Categorized People List      | [51](nip51.md) |
| 30001         | 书签Categorized Bookmark List    | [51](nip51.md) |
| 30008         | 佩戴徽章Profile Badges           | [58](nip58.md) |
| 30009         | 徽章定义Badge Definition         | [58](nip58.md) |
| 30023         | 文章Long-form Content            | [23](nip23.md) |
| 30078         | Application-specific Data        | [78](nip78.md) |
| 1000-9999     | Regular Events                   | [16](nip16.md) |
| 10000-19999   | Replaceable Events               | [16](nip16.md) |
| 20000-29999   | Ephemeral Events                 | [16](nip16.md) |
| 30000-39999   | Parameterized Replaceable Events | [33](nip33.md) |

## Message types

### Client to Relay
| type  | description                                         | NIP            |
|-------|-----------------------------------------------------|----------------|
| EVENT | used to publish events                              | [1](nip01.md)  |
| REQ   | used to request events and subscribe to new updates | [1](nip01.md)  |
| CLOSE | used to stop previous subscriptions                 | [1](nip01.md)  |
| AUTH  | used to send authentication events                  | [42](nip42.md) |
| COUNT | used to request event counts                        | [45](nip45.md) |

### Relay to Client
| type   | description                                             | NIP            |
|--------|---------------------------------------------------------|----------------|
| EVENT  | used to send events requested to clients                | [1](nip01.md)  |
| NOTICE | used to send human-readable messages to clients         | [1](nip01.md)  |
| EOSE   | used to notify clients all stored events have been sent | [1](nip01.md)  |
| OK     | used to notify clients if an EVENT was successful       | [20](nip20.md) |
| AUTH   | used to send authentication challenges                  | [42](nip42.md) |
| COUNT  | used to send requested event counts to clients          | [45](nip45.md) |

Please update these lists when proposing NIPs introducing new event kinds.

When experimenting with kinds, keep in mind the classification introduced by [NIP-16](nip16.md).

## Standardized Tags

| name       | value                   | other parameters  | NIP                           |
| ---------- | ----------------------- | ----------------- | ----------------------------- |
| e          | event id (hex)          | relay URL, marker | [1](nip01.md), [10](nip10.md)  |
| p          | pubkey (hex)            | relay URL         | [1](nip01.md)                 |
| a          | coordinates to an event | relay URL         | [33](nip33.md), [23](nip23.md) |
| r          | a reference (URL, etc)  |                   | [12](nip12.md)                |
| t          | hashtag                 |                   | [12](nip12.md)                |
| g          | geohash                 |                   | [12](nip12.md)                |
| nonce      | random                  |                   | [13](nip13.md)                |
| subject    | subject                 |                   | [14](nip14.md)                |
| d          | identifier              |                   | [33](nip33.md)                |
| expiration | unix timestamp (string) |                   | [40](nip40.md)                |

## Criteria for acceptance of NIPs

1. 它们应该在至少两个客户端和一个中继中实现——如果适用的话。
2. 它们应该有意义。
3. 它们应该是可选的和向后兼容的：必须注意，选择不实现它们的客户端和中继在与选择不实现的客户端和中继器交互时不会停止工作。
4. 做同一件事的方法不应该只有一种。
5. 其他规则将在必要时制定。

## License

All NIPs are public domain.
