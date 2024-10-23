---
description: 转账钱包端点
---

# 交易 API

## 返回特定时间段内得交易列表

<mark style="color:green;">`POST`</mark> `http://<test.api.com:port>/api/transaction/list`

游戏运营商可以通过结算时间查询来获取交易历史列表。

**Headers**

<table><thead><tr><th width="161">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key<mark style="color:red;">*</mark></td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp<mark style="color:red;">*</mark></td><td>访问API的时间戳</td></tr></tbody></table>

**Body**

<table><thead><tr><th width="161">Name</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>traceId<mark style="color:red;">*</mark></td><td>string</td><td>每个请求的唯一标识符。 (UUID)</td></tr><tr><td>startTime<mark style="color:red;">*</mark></td><td>Long</td><td>用于检索交易开始的时间戳。</td></tr><tr><td>endTime<mark style="color:red;">*</mark></td><td>Long</td><td>用于检索交易至此的时间戳。</td></tr><tr><td>page<mark style="color:red;">*</mark></td><td>Integer</td><td>页数</td></tr><tr><td>limit</td><td>Integer</td><td>页面大小。默认：10</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200: SUCCESS" %}
```json

{
    "data": {
        "total": 1,
        "data": [
            {
                "betId": "66ed36de40677ad3a7303624",
                "playerId": "c180f4c5f1be830",
                "orderId": "66ed36de40677ad3a7303624",
                "gameCode": 1002,
                "category": "BINGO",
                "currency": "USD",
                "bet": 10,
                "win": 0,
                "effectiveTurnover": 10,
                "refundAmount": 0,
                "status": 1,
                "timestamp": 1726822110737
            }    
        ]
    },
    "code": 200,
    "message": "Success"
}
```
{% endtab %}
{% endtabs %}

## 返回特定交易的详细信息

<mark style="color:green;">`POST`</mark> `http://<test.api.com:port>/api/transaction/detail`

此 API 允许游戏运营商通过提供 `betId` 并指定时间范围（使用 `fromTime` 和 `toTime` 参数，均为 UNIX 时间戳格式）来获取单笔交易的详细历史记录。

`fromTime` 和 `toTime` 之间的时间范围必须在 7 天内。如果超过 7 天，查询将失败，并且不会返回任何数据。

**Headers**

<table><thead><tr><th width="161">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key<mark style="color:red;">*</mark></td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp<mark style="color:red;">*</mark></td><td>访问API的时间戳</td></tr></tbody></table>

**Body**

<table><thead><tr><th width="161">Name</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>traceId<mark style="color:red;">*</mark></td><td>string</td><td>每个请求的唯一标识符。 (UUID)</td></tr><tr><td>startTime<mark style="color:red;">*</mark></td><td>Long</td><td>用于检索交易开始的时间戳。</td></tr><tr><td>endTime<mark style="color:red;">*</mark></td><td>Long</td><td>用于检索交易至此的时间戳。</td></tr><tr><td>betId<mark style="color:red;">*</mark></td><td>Integer</td><td>唯一标识此下注请求交易的ID。</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200：SUCCESS" %}
```json
{
    "data": {
        "betId": "66ed36de40677ad3a7303624",
        "playerId": "c180f4c5f1be830",
        "orderId": "66ed36de40677ad3a7303624",
        "gameCode": 1002,
        "category": "BINGO
        "currency": "USD",
        "bet": 10,
        "win": 0,
        "effectiveTurnover": 10,
        "refundAmount": 0,
        "status": 1,
        "timestamp": 1726822110737
    },
    "code": 200,
    "message": "Success"
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}
