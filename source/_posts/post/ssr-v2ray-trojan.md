---
title: 2020年SSR断流，V2ray被墙，Trojan？三大翻墙工具分析+一键脚本搭建安装
---

去年下半年开始 SSR 和 V2ray VMess 不断中招断流，端口一日一封，IP 批量被 ban。被 GFW 盯上的前兆是什么？复杂加密算法 + HTTPS 加密是否有一定作用？V2ray 和 Trojan 的 WebSocket + TLS 模式是最后的方案吗？

代理上网必看常见问题
新晋科技 Trojan 简介
断流与阻断快速诊断
SSR V2ray 科普分析，拯救被墙的 IP
哪种协议最隐秘
一键安装脚本
常用客户端下载
免费云服务器申请
免费代理汇总长期更新
2020 年 2 月科学上网系列持续更新中。

关于 Trojan 与 V2ray 断流
协议再好也拯救不了破网络 Trojan 亦是如此，如果发现断流、速度较慢的问题，请多地 ping 一下主机或异地测速看看：

局部阻断会丢包，完全阻断会断网，很少出现使用限速手段阻断 V2ray 流量
可以访问但是速度慢：先相信你的配置没有问题，错误的v2ray配置不会影响性能拖慢上网速度，只会完全不能用了
延迟 400ms 以内都还好，丢包率超过 15% 使用绝对有问题，自行排查，优先看主机商网络稳定性，其次看阻断问题
速度下降的太多请自行排查，重点看主机商网络稳定性
使用域名的自行排查域名 DNS 解析质量，可能你的主机只有 100ms 延迟，但是解析你的接入点域名就需要 2000ms 并且还会丢包，用站长工具可以测试，具体可参考 网站10倍速度优化比较
Trojan 简介 & Trojan 与 V2ray 对比
Trojan 优点	Trojan 缺点
轻量高速，性能好	客户端支持程度少
伪装性强，不易被阻断断流	Trojan 客户端仅支持 socks5，部分程序不便使用
小众，短期难识别	必须使用域名
容易上手、只需用户名密码简单方便	不支持 CDN、不支持跳转/代理
NameSilo高匿域名注册商

$0.49美元起注册，匿名安全

$1.00 NameSilo 优惠码：namesilo_$1.00点击查看

Trojan 安全性
Trojan（特洛伊木马）不使用强加密、随机模糊，直接模拟网络流量最大的 HTTPS 协议来传输数据，从而不被墙识别。

V2Ray 使用 WebSocket + TLS 时，与 Trojan 本身差异并不大。但是 Trojan 还使用了网站常用服务器 Nginx 特征，从细节上做到“以假乱真”，不过墙应该还没有那么智能吧？这个特征 V2Ray 要实现也不难。

Trojan V2ray 速度比较
根据网友实测效果，同样带宽下 Trojan 的速度比 V2ray 更快。VPS 安装 BBR 之后差距更加明显，导致 V2ray 的速度不如 Trojan 快的原因有两点：

V2ray 的 WebSocket+TLS 模式有 TCP TLS 加密与 VMess 协议加密，需要进行更多的处理；
V2ray 的 WebSocket 处理性能本身比 Trojan 性能略差。
但由于 Trojan 比较新用的人少，电脑和手机的客户端上 Trojan 的支持都没有 V2ray 好，这个可以先从客户端上看支持情况，再决定要不要上。

一句话，咱差的不是 500MB/s 与 600MB/s 那 100MB 的速度，咱差的是能跑满 500MB 的线路。

哪种协议最隐秘 SSR vs V2ray
远古时代使用标准 VPN 协议的梯子已经落后了，VPN 流量太明显，当下的科学上网方式无非也就加密流量、伪装流量两种。

网传 GFW 已经通过机器学习、随机预测算法精准识别 SS 流量，加密流量集体翻车已经成为常态，未来梯子最本质的发展方向应该是无限接近“正常使用”才能正常使用。

封装流量
SSR、V2ray 协议这种类型，将网络流量加密封装成小众的 TCP 数据包（Socket5、VMess），V2ray 流量识别已被申请专利

缺点：没有明显特征，但是从墙的角度来看小众、未知的数据流量就是最明显的特征，使用代理的流量在运营商层面都会显示 TCP 未知流量，如果没有使用 TLS 加密则可以分析识别流量数据

加密流量
将网络流量加密并伪装成正常的 HTTPS 流量，与平时访问网站的流量形态是一样的。

优点：HTTP 较为大众，海量正常流量中很难找出梯子流量，找到也几乎无法分析流量内容， GFW 不会贸然的去阻断疑似流量。

通俗的比较
假如在一条车流量很大的大路上

用 HTTP 的都是窗户透明型号统一的出租车
用 HTTPS 的都是窗户不透明型号统一的出租车
用 SS/SSR/V2Ray 原协议的都是一些窗户不透明的私家车
SS/SSR 用 HTTP/TLS 混淆的都是把私家车染成了出租车的样子
用 VPN 的都是坐的大巴，虽然关着窗但知道这肯定是大巴。
总结来说 V2ray WS + TLS 是最安全隐秘的。

引用自 @Janet's grow up

SSR V2ray 封禁前兆
SSR 和 V2ray 的简介与比较就不再赘述，总的使用情况来看 SSR 已经很被动，V2ray 的 VMess 也岌岌可危。

就自己和身边朋友使用情况来看：

特殊时期会议、净网行动等开始有行动；
流量异常的 IP 段重点监控，容易中枪（如 Vultr Tokey）；
初期数据量较大的时候被阻断，访问降速、错误；
SSR 被盯上起初是封禁端口，几次端口封禁后直接封禁 IP。
IP 被封禁后直接的解决办法就是更换 IP，这个免不了要花心思掏银子。所以一旦端口被封就要引起注意，适时地切换协议或者暂停使用一段时间。

特殊时期 v2ray 端口被封就立马收手，缓一缓再用，换端口存活时间不会太久。

加上 Nginx 反代和 CDN 可以缓解一下，但大多数都是 IP 段被封的。

IP 被墙检测判断
最简单的判断方法是 Ping 一下，如果通了万事大吉，如果没通就没法判断到底是墙引起的还是 VPS 自身的问题，因此需要借助以下工具判断：

ping.pe
SSR V2ray 端口被封
搬瓦工被墙检测
ping.pe 从网络层面进行检测，访问 http://ping.pe/，输入你的 IP 进行测试，如果国内大面积红色就说明被墙了。也可以在右上角切换使用 port 进行端口被封测试。

点击打开

image-20200218144019123

V2ray 国内跳转加速
鉴于中国地大物博，各种运营商群雄割据，大部分国外线路都受运营商类型、所在省份影响：

同样是中国电信，同一条线路可能从武汉访问就比成都要快
同一条线路，电信访问通常比移动联通都要快
借助 V2ray 的代理转发特性，大多数机场都发明了跳转加速：

你(移动) —> 武汉某国内服务器(电信) —> 国外

我们知道国内访问国内速度是很快的，“先到国内”这样就把运营商和地域差异抹平了，保证关键的 国内 —> 国外 线路是质量最优的。

优点	缺点
抹平运营商与地域差异，真的很快	成本太大，需要额外的国内服务器
机场用的比较多	个人用着没必要，可以根据自身情况针对性选择线路
CDN 拯救被墙的 IP - V2ray
对于使用 HTTP/WebSocket 传输的流量，可以使用 CDN 进行“反向代理”绕过墙。在这个场景下 CDN 相当于另一台国外的 VPS。

网站加速

CDN 原理 - 腾讯云 CDN 应用场景
之所以 IP 被墙，是因为用户和 VPS 是直连经过墙的，流量集中、特征明显的时候墙就会阻断 IP。如果使用 CDN，墙只知道你请求到 CDN，和众多普通应用一样，不知道具体后面的 VPS，无法有效禁止；同时 CDN 大规模商用，视地域、状态有很多 IP 地址，墙不会轻易去屏蔽。

V2ray 使用 CDN 的三个条件
HTTP/WebSocket 流量：CDN 专为 HTTP 及其衍生协议设计进行网站、下载加速，因此只有 HTTP/WebSocket 协议才能使用
需要有自己的域名：CDN 基于域名加速，需要购买单独的域名，这个问题好解决，一些域名后缀首年只需个位数
需要一个 CDN 服务商：腾讯云、阿里云均有一定的免费 CDN 额度，即便收费费用也还行，但是需要域名备案很复杂，因此使用国外 CDN 服务商比较好，推荐使用 CloudFlare
2ray 使用 CDN

V2ray 使用 CDN 的优缺点
优点：

能够有效防止被墙
已经被墙的可以通过 CDN “起死回生”
对于慢的线路有一定的加速效果，CDN 本身走的就是最优线路
缺点：

延迟会有一定影响，多了一层代理，速度可能起减速效果
配置繁琐（本站后续会整理精品教程）
需要单独域名
如果 IP 被墙了那就直接用，没被墙可以多测试测试再决定要不要使用 CDN 进行 V2ray 加速。

科学上网必看
科普一下科学上网原理
国内可以自由访问到国外大部分服务器，如 亚马逊

不符合法律法规，国内政策如色情、反动、非客观内容或者有类似潜力不可控因素的站点与内容进行人为限制，数据包出国的时候识别检查拦截下来

国内可以先访问国外能访问的服务器，那台服务器作为代理人，代理了你的访问请求把访问结果返回给你，成功实现代理上网（绿色部分）
GFW 过滤原理 

科学上网浅谈
防火墙存在有一定的意义，国外一些产品确实有一点点别有用心，譬如早年 2014 前后我上 YouTube 推荐的都是政治相关视频；有一段时期 Google Play 上面色情小说 App 泛滥成灾；一直到现在美国之音等媒体井底之蛙或者别有用心的眼光来看国内的事件。

但我觉得科学上网在大陆最主要的作用其实还是用来网络加速和提高工作效率，一是某些国外的服务网速实在差的不行，另外就是可以替代国内做的不好的产品如百度搜索，剩下的才是来探究知识：

Google 世界第一大搜索引擎，YouTube 世界第二大搜索引擎
留学申请，欧洲那一片尤其英国高校官网的速度太慢
Github、开源软件网站等网速太慢，KB 级别的速度极大的降低工作效率
YouTube 上有很多优质的视频和广告 P:)
Google 搜索的收录率、搜索质量等都出奇的好，譬如本站仅有 Google 收录了
每个人都应该有自己的分辨能力，需要对一些观点、资讯保留自己合理的认知，然后做到合理的信息传播。无论你身处于哪个国家/地区，请遵守当地区域法律法规与民族习惯，严禁从事违法犯罪以及煽动不实言论活动。

V2ray 简介
SS 用的时间比较久，本文不做赘述，我是在去年 11 月 SS 被墙之后才了解使用 V2ray 的。

V2ray 特性官网已经介绍的很清楚了：

多入口多出口: 一个 V2Ray 进程可并发支持多个入站和出站协议，每个协议可独立工作。
可定制化路由: 入站流量可按配置由不同的出口发出。轻松实现按区域或按域名分流，以达到最优的网络性能。
多协议支持: V2Ray 可同时开启多个协议支持，包括 Socks、HTTP、Shadowsocks、VMess 等。每个协议可单独设置传输载体，比如 TCP、mKCP、WebSocket 等。
隐蔽性: V2Ray 的节点可以伪装成正常的网站（HTTPS），将其流量与正常的网页流量混淆，以避开第三方干扰。
反向代理: 通用的反向代理支持，可实现内网穿透功能。
多平台支持: 原生支持所有常见平台，如 Windows、Mac OS、Linux，并已有第三方支持移动平台。
总结来说 V2ray 有很多先进的点，VMess 可能还算容易被识别破解，但是 WebSocket + TLS 模式在未来很长一段时间应该都没问题。

服务器对科学上网的影响
服务器线路是最重要的，选择科学上网服务器线路最核心的点就是：带宽 >= 丢包率 > 延迟

带宽决定一切，有些服务商带宽降到了三位数 KB，YouTube 480p 都撑不起来
一定要下载测试文件看看速度怎么样，举个例子 Vultr Tokey 到西南电信均速只有 128KB，加锐速也没用
一定要在多个时间段测试下载速率
丢包率影响响应时间，额外的重传变相削弱了带宽，> 30% 时多少都会有问题
同一条线路不同时间段丢包率不一样
应当关注用网高峰期比如晚上的丢包率
对于延迟，不高于 400ms 我觉得非即时类应用都还行
同一条线路不同时间段延迟不一样
CN2 涨价？VPS 选购位置|线路|流量全面分析 PK 机场 附 VPS 服务商用户量数据

代理上网必看常见问题
搭建篇
Q: SSR 用不了，按照步骤操作无效
A: 检查 SS 服务端有没有问题，端口、IP ping 通；检查客户端有无启动，监听端口正不正确；检查代理设置有没有动过，一般是 1080

…持续更新

机场篇
Q: 机场网站打不开了
A: 有可能是这个机场被墙了，打开代理上网模式来访问看看，换个时间段来访问看看，可能在维护，如果还不行，那就是机场跑路了┓( ´∀` )┏

Q: 机场注册不了，收不到邮件
A: 垃圾邮件里面查看一下

Q: 代理上网速度慢
A: 刚开始的时候人比较少机场速度可能会比较快一点，一但用的人比较多或者高峰期，速度有可能

Q: 会不会泄露个人隐私
A: 理论上通常情况下 TLS 加密的流量比如 HTTPS 站点是没有问题的，非加密流量可以扒的底裤都不剩，看机场主良心了。
