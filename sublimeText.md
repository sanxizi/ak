# sublimeText3 sftp插件配置

**功能**：实现本地代码与线上环境代码的同步，可设置本地保存直接提交同步，即本地保存代码时同步更新云端代码，实现本地开发，线上观测结果。因线上统一使用docker环境配置，故不存在因环境差异而出现的bug。



### 1. 安装package control

最简单的方式是通过Sublime Text 3的console命令界面进行安装

使用 ctrl+`快捷键 或者 菜单项View > Show Console 来调出命令界面

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587435899521-320a8cdb-02e8-41dd-8d97-02151c1df62f.png)

然后复制粘贴下面的Python代码到命令输入框中:

```python
import
 urllib.request,os,hashlib; h = '7183a2d3e96f11eeadd761d777e62404' + 
'e330c659d4bb41d3bdf022e94cab3cd0'; pf = 'Package 
Control.sublime-package'; ipp = sublime.installed_packages_path(); 
urllib.request.install_opener( urllib.request.build_opener( 
urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 
'http://sublime.wbond.net/' + pf.replace(' ', '%20')).read(); dh = 
hashlib.sha256(by).hexdigest(); print('Error validating download (got %s
 instead of %s), please try manual install' % (dh, h)) if dh != h else 
open(os.path.join( ipp, pf), 'wb' ).write(by)

```

另外提供Sublime text 2的Package Control的安装代码

```python
import
 urllib2,os,hashlib; h = '7183a2d3e96f11eeadd761d777e62404' + 
'e330c659d4bb41d3bdf022e94cab3cd0'; pf = 'Package 
Control.sublime-package'; ipp = sublime.installed_packages_path(); 
os.makedirs( ipp ) if not os.path.exists(ipp) else None; 
urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) );
 by = urllib2.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ', 
'%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join(
 ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error 
validating download (got %s instead of %s), please try manual install' %
 (dh, h) if dh != h else 'Please restart Sublime Text to finish 
installation')
```



### 2. 点击package control，选择install package，在弹出的选择框中输入sftp，选择第一项完全安装。

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587435969072-8e11b6e1-e496-45e9-b1da-ce1030ac1ef7.png)

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587435980223-b5631379-35fd-4283-9b60-c6b398fb344b.png)

### 3. 安装完成后 点file，可看到SFTP/FTP，

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587436040550-55aac7dc-d035-444d-8b13-8ad7a4cf7ceb.png)

点击Setup Server会自动生成一个配置文件，一般只需要修改 host、user、password 、remote_path，视个人情况而定

<img src="https://cdn.nlark.com/yuque/0/2020/png/200145/1587436053078-d0160317-8240-4ea2-bc82-8b9d78bd9d14.png" style="zoom:80%;" />



### 4. 使用SFTP上传项目，在工具栏中点击Project - Add Folder to Project，选择项目的文件夹。这样所选择的文件夹会出现左侧，右键project 选择SFTP->Map to Remote,自动生成一个sftp-config.json 文件。

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587436064248-b3be2387-1501-49cc-b20a-ace86546ab5b.png)



<img src="https://cdn.nlark.com/yuque/0/2020/png/200145/1587436073091-3b74dc49-5493-4174-8d0d-80afce6d20a9.png" style="zoom:67%;" />





***示例配置如下（可根据自己的方式配置）：\***

> "host": "118.xxx.xxx.36",  //宿主机地址
>
> "user": "rzwei",  //您的宿主机 ssh 账号
>
> "password": "xxx", //密码
>
> "upload_on_save": true, //保存本地文件自动代码同步到远程
>
> "remote_path": "/home/rzwei/webapp",  //您的工作目录（PHP代码）

