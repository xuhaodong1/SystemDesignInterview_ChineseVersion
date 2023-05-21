# 从 0 拓展到数百万用户

设计一个支持数百万用户系统是具有挑战性的，那是一个需要不断细化与改善的过程。在本章中，我们构建了一个支持单个用户的系统，并将其逐步拓展到服务数百万用户。读完本章后，你将会掌握可以帮助你解决系统设计面试问题的许多技能。

### 单服务器设置

千里之行始于足下，构建一个复杂的系统也不例外。从简单的开始，所有东西都都在一台服务器上运行。图 1-1 展示了所有东西都运行在一台服务器上的单服务器设置的图示：web 应用、数据库、缓存等等。

<figure><img src=".gitbook/assets/image (2).png" alt="" width="563"><figcaption><p>图 1-1</p></figcaption></figure>

探索请求流和流量源有助于帮助我们理解这些设置，我们首先观察请求流（图 1-2 ）。

<figure><img src=".gitbook/assets/image (1).png" alt="" width="563"><figcaption><p>图 1-2</p></figcaption></figure>

1. 用户通过域名访问网站，如 <mark style="color:blue;">api.mysite.com</mark>。通常来说，域名系统（ DNS ）由第三方提供的付费服务，而不会由我们的服务器托管。
2. 网络传输协议（ IP ）地址返回到浏览器或 mobile 应用。在本例中，被返回的 IP 地址是 15.125.23.214。
3. 一旦获取到 IP 地址，超文本传输协议（HTTP）<mark style="color:blue;">\[1]</mark> 请求会立即发送到你的 web 服务器上。
4. web 服务器返回 HTML 页面或者 JSON 响应用以页面渲染。

接下来，让我们观察流量源。到达 web 服务器的流量有 2 种：web 应用与 mobile 应用。

* web 应用：它结合使用服务端语言（Java、Python 等）来响应业务逻辑，存储等，以及客户端语言（HTML、JavaScript 等）来呈现页面。
* mobile 应用：HTTP 协议是 mobile 应用和 web 服务器的通信协议。由于简单，JSON 是常用的传输数据的 API 响应格式，JSON 格式的 API 响应示例如下：

<pre class="language-json"><code class="lang-json"><strong>// GET /users/12 – Retrieve user object for id = 12
</strong>{
    "id": 12,
    "firstName". "John"
    "lastName". "Smith".
    "address": {
        "streetAddress". "21 2nd Street"
        "city": "New York"
        "state": "NY"
        "postalCode": 10021
    }
    "phoneNumbers": [
        "212 555-1234"
<strong>        "646 555-4567"
</strong>    ]
}
</code></pre>

### 数据库

