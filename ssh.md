# gitlab配置ssh-key 免密码上传下载 



#### windows环境下

1. 打开本地git bash,使用如下命令生成ssh公钥和私钥对
`ssh-keygen -t rsa -C 'xxx@xxx.com'` 然后一路回车(-C 参数是你的邮箱地址)

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587526955895-8026e164-027e-45ab-8587-40c7438072ff.png)

2. 然后打开~/.ssh/id_rsa.pub文件(~表示用户目录，比如我的windows就是C:\Users\Administrator)，复制其中的内容

3. 打开gitlab,找到Profile Settings-->SSH Keys--->Add SSH Key,并把上一步中复制的内容粘贴到Key所对应的文本框，在Title对应的文本框中给这个sshkey设置一个名字，点击Add key按钮

![](https://cdn.nlark.com/yuque/0/2020/png/200145/1587526955958-bc474e3d-0afd-4bc0-85cb-5cb8f5a435f7.png)



#### Linux环境下

```
1》首先，你得在root目录下

cd /root
```

![img](https://img2018.cnblogs.com/blog/978388/201903/978388-20190321104359119-817791768.png)

 

```
2》查看是否已经存在SSH-Key【其实就是查看.ssh这个隐藏目录是否存在】

ls -al ~/.ssh
```

![img](https://img2018.cnblogs.com/blog/978388/201903/978388-20190321104602081-1170269408.png)

如果没有就新建，如果有，建议删除再新建

```
删除命令【其实就是删除.ssh这个隐藏目录目录】

rm -rf .ssh
```

 

```
3》新生成SSH-key【替换成你自己的邮箱】

ssh-keygen -t rsa -C "sxd4business@qq.com"
```

键入命令后，会让你输入密码用来保护你的密钥等，总共三次需要输入的，直接三次回车就好

【关键是，设置了你自己以后忘了就得重新生成】

【-C 是给你的密钥设置注释，你不想设置为邮箱，设置成别的也行】

![img](https://img2018.cnblogs.com/blog/978388/201903/978388-20190321105216644-7490050.png)

 

```
4》生成后，会在/root目录下，也就是当前用户的目录下，生成一个.ssh隐藏目录，目录中会有【id_rsa】和【id_rsa.pub】两个文件，一个是私钥，一个是公钥。你现在就可以复制使用了
```

![img](https://img2018.cnblogs.com/blog/978388/201903/978388-20190321105459763-642876596.png)

![img](https://img2018.cnblogs.com/blog/978388/201903/978388-20190321105522876-474589191.png)





参考链接：https://www.cnblogs.com/sxdcgaq8080/p/10570150.html