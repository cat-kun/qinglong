## 获取京东cookie

> 前言：如果已经安装过低版本的huayu（低于2.x版本）请先删除，没有安装的跳过此步骤，[直接开始安装huayu](#1)
>
> 1、查看程序运行中的PID
>
> ```
> ps -ajx|grep JDC
> ```
>
> ![image-20210617102646650](https://tva1.sinaimg.cn/large/008i3skNgy1grl1z44o5bj312y07cjsd.jpg)
>
> 2、结束程序（*****改为你的PID)
>
> ```
> kill -9 *****
> ```
> 例如这里是29709，那么就是` kill -9 29709`
>
> 3、删除配置文件和JDC主程序：
>
> ```
> rm -rf JDC config.toml
> ```
>
> 

#### 一、安装huayu

1、找到`ql`目录所在的路径

![image-20210617103212373](https://tva1.sinaimg.cn/large/008i3skNgy1grl24pjlunj31iq09sjst.jpg)

❗️❗️比如我这里是在根目录下，那么huayu也需要安装在和`ql`同级目录，否则后面会出错

2、下载huayu包，并且解压

如果你是amd64架构（服务器，PC等）
```
wget https://github.com/dengxiaozhen/qinglong/releases/download/2.0.3/linux_amd64.zip && unzip linux_amd64.zip
```

如果你是arm架构（N1，路由器，树莓派等）
```
wget https://github.com/dengxiaozhen/qinglong/releases/download/2.0.3/linux_arm.zip && unzip linux_arm.zip
```

[第三方下载地址](https://pan.feiji.work/s/21Tx)

3、

```
chmod 777 JDC
```

4、运行JDC

```
./JDC
```

5、这时会生成配置文件，再次运行会出现报错并退出，我们需要修改配置文件。

```
vi config.toml
```

```
#公告设置
[app]
    path            = "/ql" #青龙面板映射文件夹名称,一般为QL或ql
    QLip            = "http://127.0.0.1" #青龙面板的ip
    QLport          = "5700" #青龙面板的端口，默认为5700
    notice          = "使用京东扫描二维码登录" #公告/说明
    pushQr          = "" #消息推送二维码链接
    logName         = "chinnkarahoi_jd_scripts_jd_bean_change" #日志脚本名称
    allowAdd        = 0 #是否允许添加账号（0允许1不允许）不允许添加时则只允许已有账号登录
    allowNum        = 99 #允许添加账号的最大数量,-1为不限制

#web服务设置

[server]
    address         = ":5701" #端口号设置
    serverRoot      = "public" #静态目录设置，请勿更改
    serverAgent     = "JDCookie" #服务端UA    
    
#模板设置
    
[viewer]
    Delimiters      = ["${", "}"] #模板标签，请勿更改
```

按字母“i”进入编辑模式，将光标移动到“QL”处，将QL修该为“/ql”注意大小写。
再按ESC键退出编辑，再输入”:wq”保存退出。

6、再次输入命令运行即可。

```
nohup ./JDC &
```

程序会自动在后台开始运行，默认端口为5701，可以使用http://ip:5701/info 打开如果显示则代表程序安装成功。（记得开放5701端口）

![image-20210617110057805](https://tva1.sinaimg.cn/large/008i3skNgy1grl2ymxbpqj30qs09iwez.jpg)

#### 二、huayu前端部署安装

1、进入`public`目录并下载前端文件
```
wget https://github.com/dengxiaozhen/qinglong/releases/download/1.0.0/dist.zip && unzip dist.zip
```

至此前端也就部署完成了，输入http://ip:5701 即可看到如下界面：

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1grl3nd2efsj31j80qk76j.jpg" alt="image-20210617112443636" style="zoom:50%;" />

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1grl3ofguocj30lx0my0yp.jpg" alt="image-20210617112545316" style="zoom:50%;" />