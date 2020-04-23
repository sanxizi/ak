# Docker认识及简单使用

**介绍：**Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。[为什么使用 Docker](http://openhub.guchele.cn:8081/basic/docker-dev-env.html)

### Docker本地安装

#### **ubuntu安装docker**

**更新软件**

`$ sudo apt update`

**安装docker-ce**

`$ sudo apt install docker-ce`

**查看是否安装成功**

`$ docker --version`

`Docker version 19.03.5, build 633a0ea838`

**配置阿里镜像源**

salmon@salmon-Lenovo-Rescuer-15ISK:~$ sudo vim /etc/docker/daemon.json

```
{
  "registry-mirrors": ["https://8oiew75v.mirror.aliyuncs.com"]
}
```

salmon@salmon-Lenovo-Rescuer-15ISK:~$ sudo systemctl daemon-reload

salmon@salmon-Lenovo-Rescuer-15ISK:~$ sudo systemctl restart docker



#### **windows安装docker**

**官网下载安装包**     [官网](https://www.docker.com/)

**阿里云仓库配置**

Setting >> Docker Engine   修改为

```
{
  "registry-mirrors": [
    "https://8oiew75v.mirror.aliyuncs.com"
  ],
  "insecure-registries": [],
  "debug": true,
  "experimental": true
}
```



安装参考链接：

https://www.cnblogs.com/zhuyunbk/p/11661033.html

https://blog.csdn.net/luanpeng825485697/article/details/80921390





#### 基本教程

https://www.runoob.com/docker/docker-tutorial.html



#### Docker 一键搭建开发环境

（Nginx + PHP7.1.0 + PHP5.6.37）

以开发机（118.xxx.xxx.36）为例，这里简称宿主机。

在此基础上安装了 Docker 应用。

您要想构建属于自己的开发环境，只需要登录宿主机执行以下命令，即刻完成（需 root 权限）。

```shell
$ /home/webserver/shell/docker/start.sh
```

**不过使用该命令前，您得查看一下命令所需要的参数，如下：**

```shell
$ /home/webserver/shell/docker/start.sh -h
```

> 该脚本仅支持 -u -p -s [-i][-d] [-n][-m] [-t] 8个参数
>
> -u: 企业邮箱用户名[必填]
>
> -p: HTTP 容器端口号[必填]
>
> -s: SSH 容器端口号[必填]
>
> -i: 宿主机 IP [可选]（默认值为: 118.xxx.xxx.36）
>
> -d: 宿主机域名[可选]（默认值为: dev.che300.com）
>
> -n: 是否创建新镜像[可选]（yes || no ; 默认值为: no）
>
> -m: 镜像名称[可选]（默认值为: nginx-php）
>
> -t: 镜像标签[可选]（默认值为: 4.1）

**使用方法:**

```shell
./start.sh -u <args...> -p <args...> -s <args...> [-i] [<args...>] [-d] [<args...>] [-n] [<args...>] [-m] [<args...>] [-t] [<args...>]
```

*注: 初始化镜像或创建新的镜像, -n 参数值必须是 yes*

示例(1) : 

```shell
./start.sh -u rzwei -p 8000 -s 22000
```

示例(2) : 

```shell
./start.sh -u rzwei -p 8000 -s 22000 -i 118.xxx.xxx.36 -d dev.che300.com -n yes -m nginx-php -t 4.1
```

> 执行完成，请妥善保管以下属于您私人的专属账号!!!
>
> 登录宿主机: ssh rzwei@118.xxx.xxx.36; 默认密码为: xxxx
>  登录您的容器: ssh rzwei@118.xxx.xxx.36 -p 22000; 默认密码为: xxxx
>
> 您的容器 root 密码: xxxx
>
> 使用方式：
>
> 1、登录您的容器，启动 Nginx.
>
> (1) 使用 Vim 进行远程开发
>
> ----直接将PHP代码检出到 /home/webserver/webapp 虚拟主机目录下
>  ----前端代码检出到 /home/webserver/static 虚拟主机目录下
>
> (2) 使用本地编辑器开发
>
> ----需要将本地的PHP代码通过 sftp 上传到 /home/webserver/webapp 虚拟主机目录下
>  ----需要将本地的前端代码通过 sftp 上传到 /home/webserver/static 虚拟主机目录下
>
> 我已经初始了部分站点的虚拟主机配置，请见您的容器 Nginx 配置目录，如:
>  nginx-php.dev.che300.com:8000
>  cp.dev.che300.com:8000
>  open.dev.che300.com:8000
>  customer.dev.che300.com:8000
>  ... 