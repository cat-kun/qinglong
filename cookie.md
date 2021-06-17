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

#### 安装huayu

1、找到`ql`目录所在的路径

![image-20210617103212373](https://tva1.sinaimg.cn/large/008i3skNgy1grl24pjlunj31iq09sjst.jpg)

❗️❗️比如我这里是在根目录下，那么huayu也需要安装在和`ql`同级目录，否则后面会出错

2、下载huayu包，并且解压

如果你是amd64架构（服务器，PC等）
```
wget https://github.com/dengxiaozhen/qinglong/blob/master/linux_amd64.zip && unzip linux_amd64.zip
```

如果你是arm架构（N1，路由器，树莓派等）
```
wget https://github.com/huayu8/JDC/releases/download/2.0.0/linux_arm.zip && unzip linux_arm.zip
```


3、