# 从 0 拓展到数百万用户

设计一个支持数百万用户系统是具有挑战性的，那是一个需要不断细化与改善的过程。在本章中，我们构建了一个支持单个用户的系统，并将其逐步拓展到服务数百万用户。读完本章后，你将会掌握可以帮助你解决系统设计面试问题的许多技能。

### 单服务器设置

千里之行始于足下，构建一个复杂的系统也不例外。从简单的开始，所有东西都都在一台服务器上运行。图 1-1 展示了所有东西都运行在一台服务器上的单服务器设置的图示：web 应用、数据库、缓存等等。

<figure><img src=".gitbook/assets/image (2).png" alt="" width="563"><figcaption><p>图 1-1</p></figcaption></figure>

探索请求流和流量源有助于帮助我们理解这些设置，我们首先观察请求流（图 1-2 ）。

<figure><img src=".gitbook/assets/image (1).png" alt="" width="563"><figcaption><p>图 1-2</p></figcaption></figure>

1. 用户通过域名访问网站，如 <mark style="color:blue;">api.mysite.com</mark>。通常来说，域名系统（DNS）由第三方提供的付费服务，而不会由我们的服务器托管。
2.
3. 3
4. 4

### 数据库

