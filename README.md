# warp-script

CloudFlare WARP 一键管理脚本

## 一键脚本

```shell
wget -N https://gitlab.com/Misaka-blog/warp-script/-/raw/main/warp.sh && bash warp.sh
```

## 常见问题

### 1. 如果我想使用全局 IPv4 / IPv6、或我想将 VPS 的出站交给 WARP 进行代理，我该是安装 WGCF 或 WARP-GO？

WGCF 和 WARP-GO 都是第三方的 CloudFlare WARP 的 Linux 应用程序。由于 WGCF 在香港、美西区域遭到 CloudFlare 的官方限制，故只能使用 WARP-GO

对于没遭到 CloudFlare 封禁的大部分区域的建议：WGCF > WARP-GO

### 2. 如果我仅使用 socks5 代理模式，我该是安装 WARP-Cli 或 WireProxy？

WARP-Cli 是由 CloudFlare 官方提供的 Linux 客户端，但是目前仅支持 AMD64 的 CPU 架构；WireProxy 是支持 WireGuard 协议的 socks5 代理程序（类似 xray、sing-box 等）。由于脚本使用 WGCF 进行申请 WARP 账号并且生成配置文件、但是由于 WGCF 在香港、美西区域遭到 CloudFlare 的官方限制，如为CPU 架构为 AMD64 的VPS、只能使用 WARP-Cli、如为非 AMD64 的 CPU 架构只能等候 CloudFlare 对 WARP-Cli 的重视并开发

对于没遭到 CloudFlare 封禁的大部分区域、且 CPU 架构为 AMD64 的建议：WARP-Cli > WireProxy

### 3. 对于直接使用 WireGuard / Sing-box WARP 节点的

可使用本脚本的 11 选项进行提取。如果你不想在 VPS 安装 WARP 或者是没有 VPS 的用户，可从下面两个 repl 的其中之一提取

WGCF：https://replit.com/@misaka-blog/wgcf-profile-generator

WARP-GO：https://replit.com/@misaka-blog/warpgo-profile-generator

Sing-box：https://replit.com/@misaka-blog/warpgo-sbfile-generator

> 由于配置文件是由服务器生成的，并且每位用户的网络环境不一样，故不会帮助用户设置优选 WARP Endpoint IP。可参考此方法：https://blog.misaka.rest/2023/03/12/cf-warp-yxip/ 优选可用的 Endpoint IP 并替换 engage.cloudflareclient.com:2408 为自己本地网络环境可用的 WARP Endpoint IP

### 4. 在部分 IPv6 Only 的机器安装 WGCF-WARP

运行本脚本代码安装 WARP 之后，由于 EndPoint 不清楚是上游原因还是啥情况被屏蔽了，需要修改 EndPoint IP 以使用

下面是一键修改命令：

```shell
wg-quick down wgcf
echo "Endpoint = [2001:67c:2b0:db32:0:1:a29f:c001]:2408" >> /etc/wireguard/wgcf.conf
wg-quick up wgcf
curl -4 ip.p3terx.com
```

待回显出现 104 或 8 开头的 IP 即为成功

> 注：由于此地址是 DNS64 对 IPv4 的 WARP Endpoint IP 转换的 IPv6 地址，受制于 DNS64 的服务器速度限制，实际跑起来可能只有 20M 的速度

### 5. 我可以使用 WARP 的 IP 地址作为节点的入站地址吗？

不行，因为 CloudFlare WARP 的定位仅是 VPN，没有义务为你提供一个专属的 IP 进行服务。

### 6. 为啥 CloudFlare 有了 WARP-Cli，使用这些第三方客户端的 WARP 脚本还有什么用？

由于 WARP-Cli 的开发进度缓慢，如仅支持 AMD64 的 CPU 架构、不支持 IPv6 Only 的 VPS，所以说脚本使用了多种第三方客户端，尽力满足大多数用户的相关需求

## WARP Endpoint IP 优选脚本

### For Windows

下载地址：https://gitlab.com/Misaka-blog/warp-script/-/blob/main/files/warp-yxip/warp-yxip-win.7z

### For MacOS

```shell
wget -N https://gitlab.com/Misaka-blog/warp-script/-/raw/main/files/warp-yxip/warp-yxip-mac.sh && bash warp-yxip-mac.sh
```

### For Linux （包括安卓 Termux 和 iOS 的 iSH）

```shell
wget -N https://gitlab.com/Misaka-blog/warp-script/-/raw/main/files/warp-yxip/warp-yxip.sh && bash warp-yxip.sh
```

安卓 Termux 如无 wget 请使用以下命令安装：`pkg update && pkg install wget`

苹果 iSH 初始命令：`apk add -f openssh bash wget`，如遇更新包卡着不动输入以下命令：`sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories`

## 鸣谢项目

* Fscarmen：https://github.com/fscarmen/warp
* CloudFlare WARP：https://one.one.one.one/
* Wgcf：https://github.com/ViRb3/wgcf
* WARP-GO：https://gitlab.com/ProjectWARP/warp-go
* 某匿名大佬的 CloudFlare WARP EndPoint IP 优选工具及 WARP API

## 赞助

爱发电：https://afdian.net/a/Misaka-blog

![afdian-MisakaNo の 小破站](https://user-images.githubusercontent.com/122191366/211533469-351009fb-9ae8-4601-992a-abbf54665b68.jpg)
