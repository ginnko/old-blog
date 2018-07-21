---
layout: post
title: http查漏补缺之二 《cookie》
date: 2018-07-21
tag: http
---

[mdn地址](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)

1. set-cookie响应头部

    服务器使用Set-Cookie响应头部向用户代理（一般是浏览器）发送Cookie信息。

    写法：

    ```
    Set-Cookie: <cookie名>=<cookie值>
    ```

2. cookie请求头部

    现在，对该服务器发起的每一次新请求，浏览器都会将之前保存的Cookie信息通过Cookie请求头部再发送给服务器。

3. 会话期cookie

    会话期Cookie是最简单的Cookie：浏览器关闭之后它会被自动删除，也就是说它仅在会话期内有效。会话期Cookie不需要指定过期时间（Expires）或者有效期（Max-Age）。

    **当Cookie的过期时间被设定时，设定的日期和时间只与客户端相关，而不是服务端。**