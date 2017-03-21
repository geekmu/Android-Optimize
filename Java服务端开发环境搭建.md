##Java服务端开发环境搭建
###0 JDK下载安装
1. 进入源码存放目录（eg：cd /data/src）
2. wget下载jdk，由于wget不支持重定向，所以需要添加header（eg:wget --no-cookie --header "Cookie: oraclelicense=accept-securebackup-cookie" [jdk](http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.tar.gz)）
3. mv 下载的jdk压缩包到 安装目录（eg：mv jdk.tar.gz /usr/local/java）
4. 解压安装包(eg:tar zxvf jdk.tar.gz)
5. 运行 java -version 验证是否安装成功

###1 配置环境变量
这里介绍两种常用的环境变量配置方法：  
1. 修改/etc/profile文件:  
如果你的计算机仅仅作为开发使用时推荐使用这种方法，因为所有用户的shell都有权使用这些环境变量，可能会给系统带来安全性问题。 

    1. 打开环境变量配置文件（eg:vi /etc/profile）  
    2. 在文件尾追加   
        JAVA_HOME=/usr/local/java/jdk1.8.0_121  
        CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar  
        PATH=$JAVA_HOME/bin:$PATH  
        export JAVA_HOME  
        export CLASSPATH  
    3. 使用source命令启用配置（eg:source /etc/profile）

2. 修改.bashrc文件：  
这种方法更为安全，它可以把使用这些环境变量的权限控制到用户级别。  

    1. 打开用户目录的.bashrc文件（eg:vi ~/.bashrc）  
    2. 在文件尾追加  
        JAVA_HOME=/usr/local/java/jdk1.8.0_121  
        CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar  
        PATH=$JAVA_HOME/bin:$PATH  
        export JAVA_HOME  
        export CLASSPATH  
    3. 退出重新登录

###2 环境测试
1. 在任意目录，通常在/data/tmp目录新建一个java文件（eg:Demo.java）
2. 编译代码，javac Demo.java
3. 运行代码，java Demo

###3 常见问题
“Error: Could not find or load main class”

1. 如果java代码里面没有设置package，则是环境变量配置有误；
2. 如果java代码里面有设置package，则需要构建和包名一致的路径，eg:package com.cjh.demo,则需要构建com/cjh/demo目录，并把编译的class文件放到该目录，然后回到和com平级的目录里面运行