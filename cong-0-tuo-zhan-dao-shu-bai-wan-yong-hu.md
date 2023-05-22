# 从 0 拓展到数百万用户

设计一个支持数百万用户系统是具有挑战性的，那是一个需要不断细化与改善的过程。在本章中，我们构建了一个支持单个用户的系统，并将其逐步拓展到服务数百万用户。读完本章后，你将会掌握可以帮助你解决系统设计面试问题的许多技能。

### 单服务器设置

千里之行始于足下，构建一个复杂的系统也不例外。从简单的开始，所有东西都都在一台服务器上运行。图 1-1 展示了所有东西都运行在一台服务器上的单服务器设置的图示：web 应用、数据库、缓存等等。

<figure><img src=".gitbook/assets/image (2).png" alt="" width="563"><figcaption><p>图 1-1</p></figcaption></figure>

探索请求流和流量源有助于帮助我们理解这些设置，我们首先观察请求流（图 1-2 ）。

<figure><img src=".gitbook/assets/image (1) (1).png" alt="" width="563"><figcaption><p>图 1-2</p></figcaption></figure>

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

随着用户基数的增长，一台服务器已经不够用了，我们需要多个服务器：一个用于处理 web / mobile 的流量，另一台则用于数据库（图 1-3）。将 web / mobile 流量（网络层）与数据库（数据层）的服务器分隔开有助于让它们独立拓展。

<figure><img src=".gitbook/assets/image (1).png" alt="" width="563"><figcaption><p>图 1-3</p></figcaption></figure>

#### 如何选择数据库

你可以选择传统的关系型数据库和非关系型数据库，让我们来看看它们有何不同。

关系型数据库也称为关系型数据库管理系统或者 SQL 数据库**。**最流行的有：MySQL、Oracle、PostgreSQL 等。关系型数据库以表格和行的形式表示和呈现数据，你可以使用 SQL 跨越不同的数据库表执行连接操作。

非关系型数据库也称为 NoSQL 数据库。最流行的有：CouchDB、Neo4j、Cassandra、HBase、Amazon Dynamo DB 等。这些数据库被分为 4 类：键值存储、图存储、列存储和文档存储，非关系型数据库通常不支持连接操作。

对于大多数开发者而言，关系型数据库是最佳选择，因为它已经存在了 40 多年，并且仍运行良好。然而，如果关系型数据库不适用于你的特定使用情况，探索关系型数据库之外的领域至关重要，下面列出非关系型数据库的适用情况：

* 你的应用需要超低延迟
* 你的数据是非结构化的，或者你没有任何关系性数据
* 你只需要序列化和反序列化数据（JSON、XML、YAML 等）
* 你需要存储海量数据

#### 垂直拓展与水平拓展



### 负载均衡

