---
description: Seamless wallet endpoints
---

# 钱包 API

## 检查玩家钱包余额

<mark style="color:green;">`POST`</mark> `http://<test.api.com:port>/api/bank/balance`

由运营商实现。集成系统将调用此端点以检索用户的最新钱包余额。

**Headers**

<table><thead><tr><th width="173">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key<mark style="color:red;">*</mark></td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp<mark style="color:red;">*</mark></td><td>访问API的时间戳</td></tr></tbody></table>

**Body**

<table><thead><tr><th width="162">Name</th><th width="110">Type</th><th>Description</th></tr></thead><tbody><tr><td>traceId<mark style="color:red;">*</mark></td><td>String</td><td>每个请求的唯一标识符。 (UUID)</td></tr><tr><td>playerId<mark style="color:red;">*</mark></td><td>Number</td><td>运营商系统中的用户名。</td></tr><tr><td>currency<mark style="color:red;">*</mark></td><td>Number</td><td>币种</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200: 请求成功" %}
```json
{
    "traceId": "uuid",
    "data": {
        "balance": 5000,
        "currency": "QC",
        "playerId": "c180f4c5f1be830"
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



## 请求向玩家钱包存入额度

<mark style="color:green;">`POST`</mark>  `http://<test.api.com:port>/api/bank/deposit`

**重要提示**: referenceId 是每笔交易的唯一标识符。运营商需要为每个转账请求发送新的 referenceId。

在考虑重新发送转账请求之前，建议运营商使用 '`/bank/getsingletransaction`' 端点验证交易状态，以防出现其他失败情况。

**Headers**

<table><thead><tr><th width="173">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key<mark style="color:red;">*</mark></td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp<mark style="color:red;">*</mark></td><td>访问API的时间戳</td></tr></tbody></table>

**Body**

<table><thead><tr><th width="174">Name</th><th width="96">Type</th><th>Description</th></tr></thead><tbody><tr><td>traceId<mark style="color:red;">*</mark></td><td>String</td><td>每个请求的唯一标识符。 (UUID)</td></tr><tr><td>playerId<mark style="color:red;">*</mark></td><td>String</td><td>运营商系统中用户的用户名</td></tr><tr><td>currency<mark style="color:red;">*</mark></td><td>String</td><td>币种</td></tr><tr><td>transferAmount<mark style="color:red;">*</mark></td><td>String</td><td>转账金额（最多8位小数，但不得低于0.00000001）</td></tr><tr><td>referenceId<mark style="color:red;">*</mark></td><td>String</td><td>由运营商系统为每个API请求生成的通用唯一标识符（UUID）。</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200: SUCCESS" %}
```json
{
    "traceId": "uuid",
    "data": {
        "referenceId": "uuid2",
        "transactionId": "e5f0e860-52ee-4650-b862-f442a5d30bbc",
        "playerId": "c180f4c5f1be830",
        "currency": "QC",
        "beforeBalance": 5000,
        "afterBalance": 5100,
        "transferAmount": 100,
        "timestamp": 1729582853216
    },
    "code": 200,
    "message": "Success"
}
```
{% endtab %}

{% tab title="200: 签名验证失败" %}
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

{% tab title="200：游戏进行中" %}
```json
{
    "traceId": "uuid",
    "code": 100003,
    "message": "Trading in progress",
    "path": "/api/bank/deposit",
    "timestamp": "2024-10-22T09:35:39.842Z"
}：
```
{% endtab %}
{% endtabs %}

## 请求从玩家钱包提取额度

<mark style="color:green;">`POST`</mark>  `http://<test.api.com:port>/api/bank/withdraw`

**重要提示**: referenceId 是每笔交易的唯一标识符。运营商需要为每个转账请求发送新的 referenceId。

在考虑重新发送转账请求之前，建议运营商使用 '`/bank/getsingletransaction`' 端点验证交易状态，以防出现其他失败情况。

**Headers**

<table><thead><tr><th width="173">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key<mark style="color:red;">*</mark></td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp<mark style="color:red;">*</mark></td><td>访问API的时间戳</td></tr></tbody></table>

**Body**

<table><thead><tr><th width="181">Name</th><th width="93">Type</th><th>Description</th></tr></thead><tbody><tr><td>traceId<mark style="color:red;">*</mark></td><td>String</td><td>每个请求的唯一标识符。 (UUID)</td></tr><tr><td>playerId<mark style="color:red;">*</mark></td><td>String</td><td>运营商系统中用户的用户名</td></tr><tr><td>currency<mark style="color:red;">*</mark></td><td>String</td><td>币种</td></tr><tr><td>transferAmount<mark style="color:red;">*</mark></td><td>String</td><td>转账金额（最多8位小数，但不得低于0.00000001）</td></tr><tr><td>referenceId<mark style="color:red;">*</mark></td><td>String</td><td>由运营商系统为每个API请求生成的通用唯一标识符（UUID）。</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200: SUCCESS" %}
```json
{
    "traceId": "uuid",
    "data": {
        "referenceId": "uuid2",
        "transactionId": "e5f0e860-52ee-4650-b862-f442a5d30bbc",
        "playerId": "c180f4c5f1be830",
        "currency": "QC",
        "beforeBalance": 5000,
        "afterBalance": 4900,
        "transferAmount": 100,
        "timestamp": 1729582853216
    },
    "code": 200,
    "message": "Success"
}
```
{% endtab %}

{% tab title="200: 验证失败" %}
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

## 通过referenceId检索玩家的单笔存入/提取记录

<mark style="color:green;">`POST`</mark>  `http://<test.api.com:port>/api/bank/withdraw`

响应参数可能会根据不同的状态而变化

transactionStatus (交易状态): PROCESSING(处理中)/SUCCESS(成功)/FAIL(失败)

transactionType (交易类型): DEPOSIT(存款)/WITHDRAWAL(取款)

**Headers**

<table><thead><tr><th width="173">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key<mark style="color:red;">*</mark></td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp<mark style="color:red;">*</mark></td><td>访问API的时间戳</td></tr></tbody></table>

**Body**

<table><thead><tr><th width="170">Name</th><th width="102">Type</th><th>Description</th></tr></thead><tbody><tr><td>traceId<mark style="color:red;">*</mark></td><td>String</td><td>每个请求的唯一标识符。 (UUID)</td></tr><tr><td>playerId<mark style="color:red;">*</mark></td><td>String</td><td>运营商系统中用户的用户名</td></tr><tr><td>currency<mark style="color:red;">*</mark></td><td>String</td><td>币种</td></tr><tr><td>referenceId<mark style="color:red;">*</mark></td><td>String</td><td>由运营商系统为每个API请求生成的通用唯一标识符（UUID）。</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200: SUCCESS" %}
```json
{
    "traceId": "uuid",
    "data": {
        "playerId": "c180f4c5f1be830",
        "transactionId": "f80de91f-7185-46fb-aeeb-0f67404cb4de",
        "referenceId": "9eff88b6-41bf-40d1-b593-32c95d4b362c",
        "transactionType": "DEPOSIT",
        "transactionStatus": "SUCCESS",
        "currency": "QC",
        "transferAmount": 100,
        "beforeBalance": 5600,
        "afterBalance": 5700
        "timestamp": 1729496614023
    },
    "code": 200,
    "message": "Success"
}
```
{% endtab %}

{% tab title="200: 验证失败" %}
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
