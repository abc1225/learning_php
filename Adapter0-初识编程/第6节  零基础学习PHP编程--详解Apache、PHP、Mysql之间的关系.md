# 详解Apache、PHP和Mysql之间的关系 #

----------


## 学习方法 ##

弄清楚Apache、PHP和MySQL之间的关系，对于初学者理解程序的运行过程，还是很有帮助的，学习一个新事物，要明白最基本的三个问题： 是什么、有什么、为什么，是什么指的是新事物的宏观层面的功能描述，比如学习Apache，Apache是什么？就是一个能提供Http服务的Web服务器。有什么指的是微观层面的具体功能细节，Apache有什么？Apache有虚拟主机功能，有不同的工作模式（MPM模式），有日志功能，有压缩功能，还有各种功能模块等等。为什么指的是对事物的联系和重组，这一层是对事物本质的认识有了新的理解，Apache为什么？为什么需要使用Apache？什么场景下适合使用Apache？什么场景又不适合使用？能否使用其它Web服务器来替代它？Apache能调用PHP解释器工作，那能否和其它的脚本解释器一起工作？等等。



## Apache、PHP和Mysql的基本理解 ##

Apache是一个Web服务器： 基于Http/Https/Websocket等协议对外部提供数据、文件的获取功能

PHP是可编程的脚本语言： 提供基本的运算和逻辑处理的功能，可以很好的应用于Web网站功能需求的开发

MySQL是一种关系型数据库： 用于存储、修改、获取和管理数据的工具，可以通过结构化查询语言（SQL）进行数据库的管理


## Apache和PHP之间的关系 ##

![Http请求流程](./imgs/2018_05_18_x_001.png)

Apache和PHP解释器之间的关系，是调用和被调用之间的关系，Apache主动调用PHP解释器去执行PHP脚本文件，PHP解释器被Apache调用。

Apache是web服务器软件，它可以接受来自客户端的Http/Https等协议的请求，当请求的文件是PHP脚本文件时，它会调用PHP解释器去解释和执行该脚本中的内容，并将解释器返回的结果，根据对应的协议规则封装成相应格式的数据，再将数据返回给请求的客户端。

PHP究竟是如何被Apache调用的，可以参看第四节的《详解PHP的运行模式Sapi》，或者下一节的《详解Apache的MPM及采用的PHP模式》


## PHP和MySql之间的关系 ##

PHP和Mysql之间的关系，也是调用和被调用的关系，PHP通过SQL语言调用Mysql进行数据库的管理功能，Mysql数据库总是被动的接受操作指令。

MYSQL是小型关系数据库软件，它为可以各种软件提供数据库支持，通过PHP可以操作Mysql，同理使用其它语言也可以操作Mysql，同样PHP也可以操作其他的数据库，不一定是MYSQL。

PHP如何调用Mysql数据库进行操作？ PHP与Mysql交互使用的语言规则是SQL，但是PHP和Mysql是两个独立的应用程序，想要交互必须得先建立连接，就如同浏览器访问Web服务器一样，在请求数据发送之前也需要先成功建立tcp连接。PHP脚本与Mysql建立连接的过程都是由PHP的Mysqld/PDO等驱动来完成的，这些驱动的本质都是PHP的模块，即PHP解释器可以识别的相关函数集合，一般使用C语言编写，对PHP语言来说，屏蔽了具体连接建立和数据库协议操作的详细过程，对PHP语言暴露了一些基础的接口，即PHP可以调用到的一些数据库操作函数，如连接数据库、执行数据库SQL命令、断开连接等。

总而言之，PHP调用Mysql数据库的过程，通常是通过PHP的数据库驱动模块来操作的，它的本质也是一个网络数据的请求操作（遵循MySql通信协议来建立连接和SQL语法来执行具体操作指令）。


## Apache、PHP和Mysql的运行环境 ##

使用PHP程序就需要先搭建一个PHP的运行环境，PHP运行环境就是包含PHP+Apache+Mysql这三个软件的环境，还需要满足的条件就是，Apache可以调用PHP解释器来执行PHP脚本，PHP可以连接Mysql数据库来操作和管理存储的数据，当满足以上两个条件时，Apache、PHP和Mysql的运行环境就是一个完整的PHP运行环境了。


## 参考 ##

详解php与mysql的关系   https://blog.csdn.net/liuxuan12417/article/details/53125399

简述apache,php,mysql三者的关系    https://www.cnblogs.com/zhengwk/p/5806715.html