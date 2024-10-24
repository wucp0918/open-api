---
description: 转账钱包端点
---

# 游戏 API

## 返回游戏列表

<mark style="color:green;">`POST`</mark> `http://<test.api.com:port>/api/gameinfo/list`

游戏运营商将打开一个新窗口，使用提供的游戏URL，以便用户访问游戏。

**Headers**

<table><thead><tr><th width="173">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key<mark style="color:red;">*</mark></td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp<mark style="color:red;">*</mark></td><td>访问API的时间戳</td></tr></tbody></table>

**Body**

<table><thead><tr><th width="162">Name</th><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>traceId<mark style="color:red;">*</mark></td><td>String</td><td>每个请求的唯一标识符。 (UUID)</td></tr><tr><td>page<mark style="color:red;">*</mark></td><td>Number</td><td>页数</td></tr><tr><td>limit<mark style="color:red;">*</mark></td><td>Number</td><td>页面大小。默认：10</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "traceId": "uuid"
    "data": {
        "total": 5,
        "data": [
            {
                "name": "大富翁",
                "type": "SLOT",
                "code": 1001,
                "desc": "只是一款轻松简单的游戏，只需要投掷骰子就可以得到最多15倍的奖励，更有超级大转盘奖励，以及多种道具，丰富的游戏体验！",
                "avatarUrl": "https://<tst.api.com>/g7MQAzsTGHPFw4b.png"
            },
            {
                "name": "刮刮乐",
                "type": "BINGO",
                "code": 1002,
                "desc": "只是一款轻松简单的游戏，只需要投掷骰子就可以得到最多15倍的奖励，更有超级大转盘奖励，以及多种道具，丰富的游戏体验，等你来玩转",
                "avatarUrl": "https://<tst.api.com>/g7MQAzsTGHPFw4b.png"
            }
	]
     },
    "code": 200,
    "message": "Success"
}
```
{% endtab %}

{% tab title="error" %}
```json
{
    "traceId": "uuid",
    "code": 100000,
    "message": "param error",
    "path": "/api/gameinfo/list",
    "timestamp": "2024-10-22T06:23:16.710Z"
}
```
{% endtab %}
{% endtabs %}

## 返回游戏落地页URL

<mark style="color:green;">`POST`</mark> `http://<test.api.com:port>/api/gameurl`

游戏运营商将打开一个新窗口，使用提供的游戏URL，以便用户访问游戏。

**Headers**

<table><thead><tr><th width="173">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key<mark style="color:red;">*</mark></td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp<mark style="color:red;">*</mark></td><td>访问API的时间戳</td></tr></tbody></table>

**Body**

<table><thead><tr><th width="160">Name</th><th width="102">Type</th><th>Description</th></tr></thead><tbody><tr><td>traceId<mark style="color:red;">*</mark></td><td>String</td><td>每个请求的唯一标识符。 (UUID)</td></tr><tr><td>gameCode<mark style="color:red;">*</mark></td><td>Number</td><td>游戏码</td></tr><tr><td>playerId<mark style="color:red;">*</mark></td><td>String</td><td>运营商系统中用户的用户名</td></tr><tr><td>language<mark style="color:red;">*</mark></td><td>String</td><td>游戏应该打开的选择语言，默认EN（目前支持：ZH、EN）</td></tr><tr><td>lobbyUrl<mark style="color:red;">*</mark></td><td>String</td><td>运营商网站URL，以将用户带回游戏大厅。</td></tr><tr><td>ip<mark style="color:red;">*</mark></td><td>String</td><td>用户所在地的IP地址，可以是IPv4或IPv6格式</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200: SUCCESS" %}
```json
{
    "traceId": "uuid",
    "data": {
        "gameUrl": "http://<test.api.com:port>?code=OTU4MzU1YzMzMTBhMWVkZDdkZjBmMWNiYmRlYWQwM2Y&lang=ZH",
        "token": "958355c3310a1edd7df0f1cbbdead03f"
    },
    "code": 200,
    "message": "Success"
}
```
{% endtab %}

{% tab title="200: fail" %}
```json
{
    "traceId": "uuid",
    "code": 100002,
    "message": "signature error",
    "path": "/api/gameurl",
    "timestamp": "2024-10-22T07:09:47.377Z"
}
```
{% endtab %}
{% endtabs %}



## 终止玩家的游戏会话

<mark style="color:green;">`POST`</mark> `http://<test.api.com:port>/api/logout`

**Headers**

<table><thead><tr><th width="173">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key<mark style="color:red;">*</mark></td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp<mark style="color:red;">*</mark></td><td>访问API的时间戳</td></tr></tbody></table>

**Body**

<table><thead><tr><th width="160">Name</th><th width="102">Type</th><th>Description</th></tr></thead><tbody><tr><td>traceId<mark style="color:red;">*</mark></td><td>String</td><td>每个请求的唯一标识符。 (UUID)</td></tr><tr><td>playerId<mark style="color:red;">*</mark></td><td>String</td><td>运营商系统中用户的用户名</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200：SUCCESS" %}
```json
{
    "traceId": "uuid",
    "code": 200,
    "message": "Success"
}
```
{% endtab %}
{% endtabs %}
