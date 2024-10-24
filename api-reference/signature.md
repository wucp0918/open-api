---
icon: markdown
description: 本页面详细解释了游戏集成系统强制执行的安全设置要求。
---

# API 安全设置

在对接 此API 集成系统之前，运营商必须申请请求 API 凭证。

* API KEY - 一个唯一的 32 个字符的字母数字字符串，用于识别运营商。
* API Secret - 一个唯一的 64 个字符的字母数字字符串，用于对请求体进行签名。

## 传输层加密

运营商和游戏集成系统之间的所有通信必须通过 HTTPS 进行安全保护。

这是为了防范中间人攻击和窃听。

## 验证

Operator 必须在每次向 Game Aggregator 发送 API 调用时，在标头中携带 X-API-Key 、 X-Signature、

X-Timestamp，这样可以让集成系统验证运营商的身份。

## X-Signature

请求标头中提供的此值用于防止数据篡改。

签名是根据下方实例请求拼接参数，使用**`HMAC-SHA256`**算法后，再使用**`MD5`** 加密后返回

**请求示例**

```markdown
url： http://<test.api.com:port>/gameinfo/page:

Body：
{
    "playerId": "c180f4c5f1be830",
    "gameCode": 1001,
    "currency": "QC",
    "balance": 5000,
    "language": "ZH",
    "timestamp":"1728986462192"
}
```

**API Secret**

```markdown
813e9cb10f35c37a059c2761465781275ad641d3cb85436cdd17f08b0a6b50bf
```

拼接结果

```
/gameinfo/page/appId=b675dc0564a374e9b541b299c0177f3e&balance=5000&currency=QC&gameCode=1001&language=ZH&playerId=c180f4c5f1be830&timestamp=1728986462192
```

**生成的签名**

```markdown
3e6f527a24e76a159df9fc969f4dfc5e
```

