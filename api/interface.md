---
icon: image-landscape
description: 单一转账钱包端点
---

# API 端点

<mark style="color:red;">**以下所有API请求都需要在Headers携带以下参数，用于验证用户身份**</mark>

<table><thead><tr><th width="173">Name</th><th>Value</th></tr></thead><tbody><tr><td>Content-Type<mark style="color:red;">*</mark></td><td><code>application/json</code></td></tr><tr><td>X-Signature<mark style="color:red;">*</mark></td><td>使用HMAC-SHA256算法生成的数字签名并进行MD5加密返回，使用运营商的API秘钥对请求体进行签名。</td></tr><tr><td>X-API-Key</td><td>运营商的API密钥</td></tr><tr><td>X-Timestamp</td><td>访问api的时间戳</td></tr></tbody></table>

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>游戏API</td><td></td><td></td><td><a href="interface/game.md">game.md</a></td></tr><tr><td>钱包 API</td><td></td><td></td><td><a href="interface/bank.md">bank.md</a></td></tr><tr><td>交易 API</td><td></td><td></td><td><a href="interface/transaction.md">transaction.md</a></td></tr></tbody></table>

