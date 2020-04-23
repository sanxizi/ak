



## 基本账号介绍



#### gitlab: （项目仓库）

登陆地址：http://182.254.153.226/
账号名称：zhangc
初始密码：zhangc@che300.com

#### 宿主机：（线上初始docker环境）

地址：118.190.240.36  （使用xshell等ssh软件进行登陆远程操作）

初始账号为：zhangc

默认密码为: zhangc@dev

#### 个人容器：（个人项目开发环境）

登陆地址：118.190.240.36  （使用xshell等ssh软件进行登陆远程操作）

登陆账号： webserver

登陆端口：22043

登陆密码:：webserver@dev

访问地址：open.dev.che300.com:8043（端口号每人一个，区分私人开发环境）

#### VPN：（用于远程开发工作）

账号：salmon

密码：zc19960628

地址：www.che300.club（win10连接时填写域名即可，无需带http，否则报错）

类型：PPTP（电信网络选择此类型）





## 基本环境搭建

- 使用xshell等工具登陆个人容器
- 由于 nginx 默认未启动，您需登录自己的容器手动启动 `/etc/init.d/nginx start`
- webapp目录为项目存放访问的目录
- 使用 **git clone** 从 **gitlab** 代码库拷贝所需项目代码  ( [gitlab配置ssh-key 免密码上传下载 ](ssh.md) )
- 项目克隆至webapp后需进入执行composer install 安装依赖，否则报错
    * 如：在webapp目录下
      `cd cp.che300.com`
      `composer install`
    执行完毕即可
- 安装并配置 sftp 插件，同步本地代码到宿主机（主要实现本地代码与线上环境代码的同步，详见[sublimeText3 sftp插件配置](sublimeText.md)）



**dingjia-per与dingjia两个项目之间需要设置软链，dingjia-per的api才能执行**

到dingjia.che300.com项目下执行这个代码：

```
ln  -s ../dingjia.che300.com-per api
```





#### 命令行基本操作代码

```shell
# Nginx 启动|关闭|重新生成配置
/etc/init.d/nginx {start|stop|status|restart|condrestart|try-restart|reload|force-reload|configtest}

# Nginx 安装目录
/usr/local/opt/nginx

# Nginx 配置文件目录
/usr/local/etc/nginx

# Nginx 日志目录
/usr/local/var/log/nginx

# Nginx 虚拟主机目录
/usr/local/etc/nginx/webconfig

# Nginx 虚拟主机工作目录（家目录）
/home/webserver/webapp

# PHP7.1.0 启动|关闭
/etc/init.d/php-fpm {start|stop|force-quit|restart|reload|status|configtest}

# PHP7.1.0 安装目录
/usr/local/opt/php/7.1.0

# PHP7.1.0 配置文件目录
/usr/local/etc/php/7.1

# PHP7.1.0 fpm日志以及错误日志目录
/usr/local/var/log/php-fpm

# PHP7.1.0 扩展安装目录
/usr/local/etc/php/7.1/conf.d

# PHP5.6.37 启动|关闭
/etc/init.d/php-fpm-56 {start|stop|force-quit|restart|reload|status|configtest}

# PHP5.6.37 安装目录
/usr/local/opt/php/5.6.37

# PHP5.6.37 配置文件目录
/usr/local/etc/php/5.6

# PHP5.6.37 fpm日志以及错误日志目录
/usr/local/var/log/php-fpm

# PHP5.6.37 扩展安装目录
/usr/local/etc/php/5.6/conf.d


# 可执行文件所在目录
/usr/local/bin
```















