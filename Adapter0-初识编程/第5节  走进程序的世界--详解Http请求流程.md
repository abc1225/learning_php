# 详解Http请求流程 #

※ 由于 Hostker 已转型 IaaS 服务，此文目前对应业务仅限主机壳。

www.90.cx 这个博客将会收录我们开发过程中所涉及到的大多数技术细节。为了给大家有一个比较直观的印象，单独写一篇导航作为博客内容的导航。标题看起来就是非常大的一个坑，因此接下来就只挑选与我们技术相关的部分来说说。

以下每一个《书名号》括起来的标题将会是一篇文章，如果暂时没有链接到文章，那么就是一个坑待填。

DNS 查询

在浏览器敲下 www.90.cx 并回车，浏览器将会发起 DNS 查询，从根（.）开始，直到 www.90.cx. 取得 A 记录上的 IP。具体细节点击《DNS 查询全解》查看。在分配 IP 的时候，我们的 DNS 就会负责 CDN 节点的调度任务，将用户调度到最合适的节点。具体细节点击《DNS 智能调度原理》查看。

※ 扩展阅读：对于域名邮箱有兴趣的读者，可以顺便读读《CDN 厂商都爱自架 DNS？》。

HTTP 处理

拿到了 IP 之后，需要确认协议是 HTTP 还是 HTTPS。如果是 HTTPS，需要按照《HTTPS 握手过程》进行处理。完成握手之后，浏览器将会发送请求头，类似这样：

> GET / HTTP/1.1 Host: www.90.cx User-Agent: Mozilla/5.0 (Windows NT
> 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36 Accept-Encoding: gzip, deflate,
> sdch

HTTP 协议具体聊起来可以写出一本书，因此发起请求就只写到这里，接下来我们的 CDN 节点会接收到这个请求并进行处理，CDN 最前端是 Nginx 负责这一请求的鉴权和其它一些工作，之后转交到 Squid 进行缓存判断，如果缓存过期还需要移交到运算节点 Apache，具体过程移步《解密 Hostker&主机壳 CDN——Nginx篇》《解密 Hostker&主机壳 CDN——Squid篇》查看。静态资源可以直接读取后发给浏览器，动态请求就需要交给 PHP 处理。

PHP 运行环境

为什么我们只支持 PHP 呢？因为 PHP 是世界上最好的语言 PHP 有非常独特的运行方式（mod_php），可以直接与 Apache 合体跑起来，这是其它语言（Golang、NodeJS 等）无法做到的。具体细节点击《对比 PHP 各种运行模式》。上一节的 CDN 会把请求转发到运算节点，将会由 Apache 进行处理。在 Apache 中用户可以直接编写 .htaccess 实现 Rewrite（伪静态）、自定义响应头（HSTS、Expire 缓存控制等）、控制文件夹访问权限等等非常灵活。不需要重启 Apache 就可以自定义绝大部分功能。

在运行过程中，PHP 会涉及到安全方面的问题，因此业界使用 Cpanel、DirectAdmin 等面板的主机商均没有使用 mod_php 这个运行模式。所以我们自己开发了一套沙箱环境，对用户之间的数据访问、数据库、Memcache 等业务进行隔离保护。具体参考《Hostker 沙箱环境介绍》。

WebSocket 实时通讯

由于传统 PHP 的生命周期决定了他不适合用于长期运行，我们的共享主机环境也无法允许用户长期连续运行一个脚本。开发者遇到实时通讯场景（例如在线聊天）将会非常头疼，因此我们开发了 WebSocket 服务供开发者使用，有需要可移步 Hostker Wiki 查看开发文档。这里我们来说说如何《用 PHP 实现 WebSocket 服务》。

结束

至此，我们的任务就完成了。浏览器拿到 HTML、JS、CSS、图片等资源之后就会将内容渲染展示给访客。这部分属于前端方面的技术，我们技能点不足就不深入讨论了。今后如果遇到比较有价值并适宜公开的技术内容，我们也会发布到本博客中。



【导航篇】从输入域名到展示网页，我们都做了什么？  https://www.90.cx/init-website/


HTTP协议详解以及URL具体访问过程  http://www.cnblogs.com/phpstudy2015-6/p/6810130.html


http服务详解（1）——一次完整的http服务请求处理过程   https://www.cnblogs.com/along21/p/7691234.html



一次完整的HTTP请求过程   https://blog.csdn.net/yezitoo/article/details/78193794


一次完整的HTTP事务过程分析   https://blog.csdn.net/xianymo/article/details/46785391