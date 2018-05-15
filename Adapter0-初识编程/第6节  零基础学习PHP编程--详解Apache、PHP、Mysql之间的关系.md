# 详解Apache、PHP和Mysql之间的关系 #




现在PHP已经是广为流行的一种编程语言，而使用PHP程序就需要搭建一个PHP的运行环境，搭建PHP本地环境就是PHP+Apache+Mysql的环境，这样就可以在电脑中运行PHP程序。那么，对于PHP环境中apache、php、mysql三者之间到底是什么样的关系呢？
Apache

它是web 服务器软件。同类产品有微软的IIS等。功能是让某台电脑可以提供 www服务，本地环境下可以通过127.0.0.1这个IP来访问本地网站。

PHP

它是服务端语言解释软件。由apache软件加载以后，使apache增加解释php文件的功能，以便这台服务器可以运行php程序。访问方法如下:

地址/文件名.php。

MYSQL

它是小型关系数据库软件。它为各种软件提供数据库支持，php站点保存的数据一般都存在 MYSQL 数据库里。当然，你也可以选择其他数据库，不一定只是MYSQL，只是通常MYSQL和PHP之间的“关系”非常好。

注:该php文件必须在 apache 配置的工作目录中。不是安装目录。

dreamweaver 可视化网页编辑软件。可以用来编写大部的网站脚本程序。例如 HTML CSS ASP PHP 等。但是它仅局限于编辑代码。为可视部份提供可视化编辑。并不能运行服务端动态脚本程序，例如 ASP PHP 等需要服务端解释才能运行的网页程序。。

补充说明:如果只是从编写代码的角度而言。系统自带的记事本都可以写。不一定非得用 dreamweaver 。它用来编写 CSS HTML 还不错。写 PHP 的话就和拿记事本写没啥两样。。反正看不到运行后的效果。。
PHP环境:一台运行了 apache 的电脑，并且该 apache 已经加载了 php 。数据库不是必装软件。如果你不需要数据库可以不装。版本号不重要。新版的功能多一点。安全性好一点。

这就是php、apache、mysql三者之间的关系，了解了他们之间的关系之后，学PHP就会更容易哦。














CGI、FastCGI和PHP-FPM关系图解    https://www.awaimai.com/371.html

mod_php对比mod_fastcgi    https://www.jianshu.com/p/88682dc61ec4


[好文]mod_php和mod_fastcgi和php-fpm的介绍,对比,和性能数据    https://wenku.baidu.com/view/887de969561252d380eb6e92.html



【导航篇】从输入域名到展示网页，我们都做了什么？  https://www.90.cx/init-website/


HTTP协议详解以及URL具体访问过程  http://www.cnblogs.com/phpstudy2015-6/p/6810130.html


http服务详解（1）——一次完整的http服务请求处理过程   https://www.cnblogs.com/along21/p/7691234.html



一次完整的HTTP请求过程   https://blog.csdn.net/yezitoo/article/details/78193794


一次完整的HTTP事务过程分析   https://blog.csdn.net/xianymo/article/details/46785391