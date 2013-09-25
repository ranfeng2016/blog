# 如何在 iOS 设备上配置 hosts

## 前提

iOS 设备指的是 iPhone/iPod touch/iPad 等运行 iOS 操作系统的移动设备。

为了测试网页在这些移动设备上的表现，我们往往需要使用真实的设备去访问内网的开发/测试环境。在某些时候，服务器端严格绑定域名（不允许使用 IP 地址访问），而且这个域名往往是虚拟的域名（比如 `yoursite.dev` 之类），我们就需要在移动设备上配置 hosts。

最重要的一点，你的设备最好是已经越狱的。越狱的目的不是装盗版软件，是为了获取系统的最高权限，这样才有可能修改 hosts 这样的系统级文件。（同理，在 Android 设备上修改 hosts 文件需要获取 root 权限。）

如果无法越狱（比如你手贱把系统升级到了最高版本），则可参考本文末尾的后备方案。

## 操作步骤

首先，我们需要安装最新版的 iTunes。因为它包含了 iOS 设备的驱动程序，装了它，Windows 才能正常识别设备。

然后，我们需要安装“同步助手”。暂不去纠结这个软件是不是盗版工具，它是目前最好用的 iOS 设备的资源管理器，我们这里只需要用到它的文件管理的功能。

![tongbu](https://f.cloud.github.com/assets/1231359/1208399/64e062e6-25d0-11e3-9b06-772b67deb3a6.png)

进入文件管理界面，进入 `/etc` 目录，可以找到 `hosts` 文件。

![file](https://f.cloud.github.com/assets/1231359/1208238/69a63b2a-25cb-11e3-958f-3d9e38308b49.png)

把它拖到桌面，就可以为所欲为了。修改完成之后，再拖回去替换原文件即可。

在修改过程中，唯一值得一提的恐怕就是换行符的格式了吧。本质上 iOS 是一个功能完备的 UNIX 系统，它的文本文件的换行符当然使用 UNIX 格式，与我们通常使用的 DOS/Windows 格式不一样。安全起见，建议你在保存文件的时候，留意换行符的格式。（参见下图）

![unix](https://f.cloud.github.com/assets/1231359/1208304/51171564-25cd-11e3-8071-02c8bc019c04.png)

## 后备方案

这里介绍两种后备方案，也适用于无法修改 hosts 的其它移动设备。

### 真实域名法

即注册一个真实的域名，解析到内网的开发/测试机。这实际上是一个变通的办法，它有一些显而易见的缺点：

* 需要花钱买域名。
* 可能需要更新服务器端的域名白名单——前端工程师往往没有这个权限。
* 域名解析通过外网 DNS 实现，比起 hosts 本地解析要慢一些。

### 代理法

在本地开发机上建一个代理服务器，让 iOS 设备通过代理服务器访问。这样域名解析这一步是在开发机完成的，只要把开发机的 hosts 配置好就可以了。

架设代理服务器并不复杂，有现成的方案，就是前端神器 Fiddler（只需要选中“允许其它机器连接”选项就可以了），顺道还可以调试移动设备的 HTTP 连接。iOS 设备端的配置也比较简单，这里就不赘述了。

***

&copy; Creative Commons BY-NC-ND 3.0 &nbsp; | &nbsp; [我要订阅](http://www.cssmagic.net/blog/subscribe) &nbsp; | &nbsp; [我要捐助](http://www.cssmagic.net/blog/donate)

&nbsp;
> * [参与评论](https://github.com/cssmagic/blog/issues/28)
> * [查看更多文章](https://github.com/cssmagic/blog/issues?state=open)