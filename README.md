# Shanxun_Linux_ZJUT
> How to connect Internet by Shanxun on Linux in ZJUT?

近来由于作死重装系统，忘记备份之前研究出的通过闪讯连接互联网的方法。

于是又经过了一个下午的研究，终于又成功连上了网。:(

以下是给使用Linux系统的浙江工业大学同学

使用**闪讯**上网的**保姆级教程**。

> 注意：使用**闪讯**即你的校园卡是 **中国电信**。而移动上网的办法还请dalao提供。
# 第一步
clone某个神奇的仓库
```bash

git clone https://github.com/Elrori/shanxun_pppoe_linux_desktop.git
```
由于年代久远等原因，这位dalao的代码**并不能**很好的运行。

我们要在安装后手动拨号。

# 第二步
1. 根据上述仓库中的描述，修改makefile文件。
注意一定要修改你的pppd版本。
查看版本：
```
pppd --version
```

2. 注释掉第81行，即*clean*代码。这一步是为了防止错误操作，导致你的*插件文件.so*被错误地清理。否则需要重新pull一遍代码，很麻烦。

3. 安装，确认没有报错，然后手动拨号：

```
pppd noauth nodetach defaultroute usepeerdns maxfail 1 user <your username> password <your password> mtu 1492 mru 1492 plugin rp-pppoe.so <network card name> plugin zhejiang_xiaoyuan_sxplugin.so
```

第三个参数那里填写的是你的网卡名称，一般说来是`enp2s0`
使用`ifconfig`命令查看你的网络设备。

4. 认证通过（会输出一个`Welcome`）修改路由表
执行
```
sudo route add default dev ppp0
```

# 感谢

直接使用了
https://github.com/Elrori/shanxun_pppoe_linux_desktop
的代码。

