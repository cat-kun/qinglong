# 青龙搭建教程

写在前面：本内容收集整理自互联网仅供技术交流之用，请勿用于任何侵犯他人权益的用途！本人不为此承担任何责任！本人与本文章所涉及的所有工具均无利益相关性，本博客为个人笔记性质不会从中获取利益，如存在侵权情况，请联系我，将会进行删除！

由于需要获取Cookie等敏感信息将存在信息泄漏以及侵权风险，以下内容本站不会提供任何可实质使用的工具站内下载，也不能为所涉及的工具承担任何使用风险，请自行甄别使用风险！

（这里以centos系统服务器为例）

[小白问答](https://github.com/dengxiaozhen/qinglong/blob/master/qa.md)

## 系统环境的准备与Docker的安装
###### 下面所有的命令都是在centos内复制粘贴回车

一、docker安装

```
sudo curl -sSL https://get.daocloud.io/docker | sh
```

二、启动docker


```
sudo systemctl start docker
```

## 青龙面板安装

一、拉取`青龙`镜像文件

```
docker pull whyour/qinglong:latest
```

二、创建容器

```
docker run -dit -v $pwd/ql/config:/ql/config -v $pwd/ql/log:/ql/log -v $pwd/ql/db:/ql/db -p 5700:5700 -e ENABLE_HANGUP=true -e ENABLE_WEB_PANEL=true --name qinglong --hostname qinglong --restart always whyour/qinglong:latest
```

三、开放青龙端口（这里以默认5700端口）

```
firewall-cmd --zone=public --add-port=5700/tcp --permanent
```

然后就可以通过ip地址+端口访问青龙控制下面板了，例如http://149.129.55.8:5700/ （这里的ip是你的服务器ip）

![image-20210612143200587](https://tva1.sinaimg.cn/large/008i3skNgy1grfv2yyq79j31fc0u0jt4.jpg)

* 默认账号密码都是admin，当你第一次登录青龙面板后，系统会自动更改你的密码。更改完密码后可以通过命令查看最新的密码

```
cat /ql/config/auth.json
```

输出的结果就是实际的密码了，当然这个密码也可以到控制面板去修改

`**{**"username":"admin","password":"******"`

到此，青龙面板就安装完了

## 面板的快速配置

一、更新青龙面板

```
docker exec -it qinglong ql update
```

![image-20210612142859085](https://tva1.sinaimg.cn/large/008i3skNgy1grfv3814z1j30u00wwael.jpg)

完成后就可以添加任务脚本了

```
docker exec -it qinglong ql repo https://ghproxy.com/https://github.com/chinnkarahoi/jd_scripts.git "jd_|jx_|getJDCookie" "activity|backUp" "^jd[^_]|USER"
```

添加完后控制面板就可以看到任务脚本了

![image-20210612143248707](https://tva1.sinaimg.cn/large/008i3skNgy1grfv3hebk7j31fc0u0jwg.jpg)

至此就配置完成了。添加好Cookie就可以正常挂机了！有错漏以及不明白的地方可以提issues https://github.com/dengxiaozhen/qinglong/issues

* 下一篇：添加cookie

## License

[MIT](https://github.com/PanJiaChen/vue-admin-template/blob/master/LICENSE) license.

[小白问答]:https://github.com/dengxiaozhen/qinglong/blob/master/qa.md
