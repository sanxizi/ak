# gitbook安装与使用

### 一、官网下载nodejs直接安装

[传送门](https://nodejs.org/en/download/)，安装完成后如下：

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587520684800-59c265a8-d4cd-40ed-a24e-1b6e7303386b.png)

可以看到npm也安装了，此时可以在cmd控制台进行验证（win+r）,输入cmd进入控制台：

```
C:\pc>node -``v
v8.``11.1
```

```
C:\pc>npm -``v
5.6``.``0
```



### 二、安装gitbook

在cmd控制台输入如下命令进行安装：

```
C:\pc>npm install gitbook-cli -g
npm WARN notice [SECURITY] 
lodash has the following vulnerability: 1 low. Go here for more details:
 https://nodesecurity.io/advisories?search=lodash&version=4.17.4 - 
Run `npm i npm@latest -g` to upgrade your npm version, and then `npm 
audit` to get more info.
C:\pc\AppData\Roaming\npm\gitbook -> C:\pc\AppData\Roaming\npm\node_modules\gitbook-cli\bin\gitbook.js
+ gitbook-cli@2.3.2
added 578 packages in 134.873s
```



 查看安装的版本：

```
C:\pc>gitbook -``V
CLI version: ``2.3``.``2
GitBook version: ``3.2``.``3
```

 

### 三、安装gitbook editor windows版 typora

下载typora

地址：https://typora.io/

https://www.typora.io/windows/typora-setup-x64.exe



### 四、使用gitbook

#### 基本使用

- **新建文件夹mybook并进入**

- `$ mkdir mybook`

  `$ cd mybook`

- **初始化**

  ` $ gitbook init`

- **启动**

  `$ gitbook serve`

- **访问**

  在浏览器输入localhost:4000



#### 扩展插件安装

gitbook安装插件的方式非常简单，只需要将所需要的插件添加到book.json中，如：

```
{
    "plugins": ["mathjax"]
}
```

然后执行：

```
gitbook install ./
```

#### GitBook目录结构

基本结构如下：

├── book.json

├── README.md

├── SUMMARY.md

├── chapter-1/

| ├── README.md

| └── something.md

└── chapter-2/

├── README.md

└── something.md

book.json：全局配置数据 （可选）

README.md：介绍电子书（必须）

SUMMARY.md：目录 （可选）

GLOSSARY.md：词汇、术语列表（可选）

 

#### SUMMARY.md格式

基本格式为：* [描述](文件路径或者http超链接)。文件路径是相对于SUMMARY.md所在的目录的。

支持多级目录，每级目录多缩进4个空格。例如：

\* [介绍](README.md)

\* [概述](index.md)

\* [接口](api.md)

\* [注意事项](note.md)

 

#### GLOSSARY.md格式

基本格式是一组h2标题加上描述，在其他页面用到这些词汇时会突出显示，鼠标放上去就会显示术语描述。术语暂不支持中文。

例如：

\## test

测试定义

 

#### book.json格式

GitBook 允许使用灵活的配置自定义电子书，这些选项在 book.json 文件中指定，格式为json。

root：包含除了 book.json外的所有电子书文件的根目录。

structure：指定readme, summary, glossary和 languages的文件名，参考 Structure paragraph。

title：电子书名，默认值是从 README 中提取出来的。在 GitBook.com 上，这个字段是预填的。

description：书籍的描述，默认值是从 README 中提取出来的。在 GitBook.com 上，这个字段是预填的。

author：作者名。在GitBook.com上，这个字段是预填的。

isbn：国际标准书号 ISBN。

language：本书的语言类型 ，默认值是 en。

direction：文本阅读顺序，可以是 rtl （从右向左）或 ltr （从左向右），默认值依赖于 language 的值。

gitbook：应该使用的GitBook版本。使用 SemVer 规范，并接受类似于 “> = 3.0.0” 的条件。

 

#### Structure paragraph

除了 root 属性之外，还可以指定readme, summary, glossary和 languages 的文件名，而不是使用默认名称，如README.md。这些文件必须在项目的根目录下，不接受的路径。

structure.readme：readme 文件名（默认值是 README.md ）

structure.summary：summary 文件名 (默认值是 SUMMARY.md)

structure.glossary：glossary 文件名(默认值是 GLOSSARY.md)

structure.languages：languages 文件名 (默认值是 LANGS.md)



#### 生成静态网站

在gitbook-demo目录下执行 gitbook build，会在gitbook-demo目录下生成一个 _book 目录，里面的内容为静态网站的文件，可以将 _book 目录下的文件拷贝到nginx、httpd等web服务器内，也可以使用gitbook serve命令启动一个web服务，默认端口是4000。

gitbook build和gitbook serve的更多用法参考gitbook help。



#### 生成目录

**问题**：

**gitbook**不支持**markdown**的`TOC`命令自动生成目录。

**解决方案**：

使用**gitbook**插件[gitbook-plugin-toc](https://www.npmjs.com/package/gitbook-plugin-toc)。
 在`book.json`中添加

```
{
    "plugins": ["toc"]
}
```

在`book.json`所在目录运行`gitbook install`，安装完成后，在使用`TOC`命令的地方使用``代替。即可自动生成文档目录。

#### 联立GitHub生成在线书籍

https://www.jianshu.com/p/4731abc562e7



简要教程

https://www.jianshu.com/p/421cc442f06c

https://www.cnblogs.com/gjb724332682/p/9290917.html



### 五、错误管理

#### 漫长等待的Installing GitBook 3.2.3

执行 gitbook -V 或 gitbook init 命令，均会显示： Installing GitBook 3.2.3 …….，之后便是漫长的等待，遥遥无期的那种，可以用 strace -ttp pid 跟踪发现其实进程还是在干活的，只是速度很慢。

##### 问题原因：

问题一：npm 默认使用安装使用的国外镜像，这个速度是比较慢的。

问题二：版本问题，3.2.3这个版本在本机可能不适用

##### 解决方案1：

问题一：切换为使用国内速度较快的淘宝镜像。

问题二：卸载3.2.3 安装3.0.0

```
# 问题一：
npm config set registry=http://registry.npm.taobao.org -g
# 问题二：
gitbook uninstall 3.2.3 #卸载
gitbook fetch 3.0.0 #安装
```

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587520859651-7ee22f98-4d47-44fb-9a6d-f1ca7685c1ef.png)

**方法2：**懒得查找可利用npm config set registry=http://registry.npm.taobao.org命令直接设置镜像



#### 使用gitbook serve 提示 Error: ENOENT: no such file or directory

Error: ENOENT: no such file or directory, stat 'C:\Users\Administrator\Desktop\gb\_book\gitbook\gitbook-plugin-highlight\ebook.css'



每次出现的错误文件还可能不一样

如：

- `Error: ENOENT: no such file or directory, stat 'd:\Mine\doc.gitbook\_book\gitbook\gitbook-plugin-fontsettings\fontsettings.js'`

##### 解决方法

修改 `C:\Users\Administrator\.gitbook\versions\3.2.3\lib\output\website\copyPluginAssets.js` 文件中的 112 行

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587521851480-b2a07630-306a-4aee-b397-12af3d8e157d.png)

将 `confirm: true` 改为 `confirm: false`



#### RangeError: Maximum call stack size exceeded

运行gitbook serve 超时

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587527837988-4c68e39a-0a40-4261-ac59-90092b0af1ce.png?x-oss-process=image/resize,w_706)

##### 解决方法：

在GitBook项目的根目录创建`book.json`，禁用`lunr`插件

**book.json**

> {
>
>   "plugins": ["-lunr"]
>
> }



参考：

https://github.com/GitbookIO/plugin-lunr/blob/master/README.md#limitations

https://cloud.tencent.com/developer/article/1441125