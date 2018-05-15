# 详解Apache、PHP和Mysql之间的关系 #



弄清楚Apache、PHP和MySQL之间的关系，对于初学者理解程序的运行过程，还是很有帮助的，学习一个新事物，要明白最基本的三个问题： 是什么、有什么、为什么，是什么指的是新事物的宏观层面的功能描述，比如学习Apache，Apache是什么？就是一个能提供Http服务的Web服务器。有什么指的是微观层面的具体功能细节，比如Apache有什么？Apache有虚拟主机功能，有不同的工作模式（MPM模式），还有日志功能，还有各种功能模块等等。为什么指的是对事物的联系和重组，这一层是对事物本质的认识有了新的理解，Apache为什么？为什么需要使用Apache，我能不能使用其它事物来替代他。



先明白一下几个定义：


PHP是后端编程语言,MySQL是数据库.

PHP和MySQL都是LAMP(Linux+Apache+MySQL+PHP)组合里的核心成员.
Linux上也有很多开发者用Nginx替代Apache配合PHP-FPM提供服务.

PHP跟MySQL的关系相当亲密,PHP从5.4开始就内置实现了MySQL驱动(mysqlnd).也就是说MySQL驱动是PHP主干代码的一部分.configure配置编译时可以直接指定mysqlnd,取代MySQL官方的libmysql:
php-src/ext/mysqlnd
--with-mysql=mysqlnd
--with-mysqli=mysqlnd
--with-pdo-mysql=mysqlnd

对比PHP添加PostgreSQL驱动:
sudo apt-get install libpq-dev
--with-pgsql=/usr/bin/pg_config
--with-pdo-pgsql=/usr/bin/pg_config
可见需要先安装PostgreSQL开发库.

PHP添加Oracle支持也跟PostgreSQL类似,需要先安装Oracle开发包(Oracle Instant Client):
Oracle Instant Client需要从Oracle官网下载.
--with-oci8=shared,instantclient,/usr/lib/oracle/11.2/client/lib
--with-pdo-oci=shared,instantclient,/usr/lib/oracle,11.2

PHP跟另一款数据库SQLite也相当亲密,因为PHP直接内置了SQLite引擎.
--with-sqlite3 默认启用
--with-pdo-sqlite 默认启用

另外,PHP从5.4开始也内置了一个单进程的用于测试和开发的HTTP服务器:
php -S localhost:8080 -t /www
执行上述命令即可建立一台监听8080端口,网站根目录为/www的,支持PHP编程和SQLite存储的HTTP服务器.
这个PHP内置的服务器相当的轻巧省资源(RES内存占用约为5MB),跑在Android手机里也不一点不费劲.

关于PHP和MySQL之间的关系解释起来很简短，但是他们之间大有用处，编写程序一点都离不开它们





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