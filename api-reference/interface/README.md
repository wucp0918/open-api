---
icon: image-landscape
description: 转账钱包端点
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# API 端点

<mark style="color:red;">**以下所有API请求都需要在Headers携带以下参数，用于验证用户身份**</mark>

<table><thead><tr><th width="173">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key<mark style="color:red;">*</mark></td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp<mark style="color:red;">*</mark></td><td>时间戳</td></tr></tbody></table>

{% content-ref url="game.md" %}
[game.md](game.md)
{% endcontent-ref %}

{% content-ref url="bank.md" %}
[bank.md](bank.md)
{% endcontent-ref %}

{% content-ref url="transaction.md" %}
[transaction.md](transaction.md)
{% endcontent-ref %}
