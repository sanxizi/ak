# 抓包与分析



### PostMan模拟请求工具

官网下载：https://www.postman.com/downloads/

使用教程：https://www.jianshu.com/p/97ba64888894（挺简单的）



### Fiddler抓包工具

腾讯软件下载：https://pc.qq.com/detail/10/detail_3330.html



#### win10下对手机App抓包

本文使用软件为fd4+win10+Android10

可参考：https://www.cnblogs.com/wasayezi/p/10131994.html

##### **电脑端配置：**

1. 安装fiddler

2. fiddler>Tools>Options>Connections 勾选Allow remote computers to connect。默认监听端口为8888（下图Fiddler listens on port就是端口号），若端口被占用可以设置成其他的，配置好后要重新启动fiddler![](https://img2018.cnblogs.com/blog/820807/201812/820807-20181217154625065-1615890441.png)

3. 配置fiddler允许监听到https（fiddler默认只抓取http格式的）

   打开Fiddler菜单项**Tools->Options->HTTPS**，

   ​     勾选**CaptureHTTPS CONNECTs**,点击Actions，

   ​     勾选**Decrypt HTTPS traffic**和**Ignore servercertificate errors**两项,点击OK（首次点击会弹出**是否信任fiddler证书和安全提示，直接点击yes**就行），见图：

![](https://img-blog.csdn.net/20160919184428770?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

##### **手机端配置：**

1. 保证手机和电脑都处于同一个网络；

2. 通过cmd，输入ipconfig查询电脑ipv4地址，或网络共享中ipv4找到，如92.168.103.53

3. 再者要知道fiddler的端口号，Tools->TelerikFiddler Options->Connections，port中值就是端口号，一般默认为8888；接下来开始操作手机；

4. 手机设置->WLAN设置->选择该wifi，点右边的箭头（有的手机是长按弹出选项框）

5. 选择修改网络配置：

   服务器主机名：与主机电脑IP地址保持一致

   服务器端口号：8888

   <img src="https://img2018.cnblogs.com/blog/820807/201812/820807-20181217154802074-1480677851.png" style="zoom:50%;" />

6. 手机端用浏览器访问http://IP：端口，用电脑的端口和fiddler设置的端口访问安装证书，访问网络，观察fiddler能否成功抓包

   ![](https://img-blog.csdn.net/20160919184529474?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

7. 点击下载之后，安装证书并起个名字，随便写就行，点击确定

   ![](https://img-blog.csdn.net/20160919184538255?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

8. 连上电脑后，手机可能连不上网，解决方式

   - 打开注册表，在HKEY_CURRENT_USER\SOFTWARE\Microsoft\Fiddler2下创建一个DWORD，值设置为80（十进制） 

![](https://img2018.cnblogs.com/blog/820807/201812/820807-20181217154857093-342614837.png)

![](https://img2018.cnblogs.com/blog/820807/201812/820807-20181217154910394-1935730721.png)

   - 编写FiddlerScript rule，点击Rules > Customize Rules,用ctr+f查找到OnBeforeRequest方法添加一行代码.

```
if (oSession.host.toLowerCase() == "webserver:8888") 
        {
            oSession.host = "webserver:80";
        }
```

![](https://img2018.cnblogs.com/blog/820807/201812/820807-20181217154945023-942852134.png)

![](https://img2018.cnblogs.com/blog/820807/201812/820807-20181217155002278-239127956.png)

9. 此时浏览器微信等app应该能连上网了，部分软件可能连不上（某些软件好像有代理限制的原因，58同城，牛课都不可以，京东淘宝可以），



#### 使用教程

https://blog.csdn.net/yue549433330/article/details/82745760