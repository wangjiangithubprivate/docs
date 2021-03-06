# 云巴特色

## 零配置无缝切换
通常，产品的业务逻辑时常会随着服务的变化而变化，比如说针对服务对象的地理位置和规模进行调整和扩展。常规的后台扩展需要进行大量的工作，来解决异地扩展机房、分布式一致性和业务分流等问题，而使用云巴的服务就完全无须有这方面的顾虑。云巴可以实现零配置的业务逻辑切换，你甚至感受不到这些改变的存在，只会觉得快。下面就介绍一下云巴是怎么做到的。

![productpng_kb_connect_step](https://raw.githubusercontent.com/yunba/docs/master/image/productpng_kb_connect_step.png)

云巴的客户端连接简要而言有三步：

1. 客户端向 tick.yunba.io 发送 DNS 请求，此时 tick 服务会根据你的 IP 获悉你的大概位置，从而返回一个就近的 ticket service 的连接信息（称为 A1）供使用。
2. 客户端获得 A1 后，会使用自身的 Appkey 和 IP 地址等信息来连接 ticket service。ticket service 通过 Appkey 的性质（付费、免费、VIP）和 IP 地址所反映的地理位置来给客户端分配它需要和云巴建立连接的前端服务器（frontend）。这个连接信息我们简称为 A2。
3. 客户端获得了 A2 以后就会去寻找对应的 frontend 建立 MQTT 或者 web socket 的连接，这样一个连接就成功建立起来了。

### 地域切换（海外服务）
选择就近的服务器来进行交互是保障实时性的重要一环，特别是需要开展海外业务的时候。云巴在上述连接过程中有两个措施来让设备连接最近的服务器：

* 首先在连接 A1 步骤的 DNS 解析阶段，服务器会给客户端返回一个较近的 ticket 服务器。
* 在 A2 阶段，ticket 也会根据 Appkey、IP 地址返回最适合的 frontend（VIP 用户返回专有线路）

### 免费／付费切换（零配置扩容）
在业务发展壮大后，需要扩容以获得更好的服务质量、更高的并发和带宽，由于云巴的上述服务选择机制，用户完全不用关心升级切换的繁琐步骤，所有通道切换都交由云巴完成。比如你需要更多的资源，我们就会让 ticket 给你返回拥有更多资源的服务器节点；又或者你想要升级现在的独享节点，我们也可以给这个节点进行动态扩容。（注：只针对付费用户）而这一切对于用户而言都是透明的，你完全不用操心。

## 跨境通信延迟低

此外，云巴还针对跨境访问的延迟问题做了优化。北美、东南亚等地的用户可以通过连接到云巴在香港的服务器，再连到深圳的服务器，从而避开延迟较高的 [GFW](https://en.wikipedia.org/wiki/Great_Firewall) 路线。

如图所示，假设在美国西海岸的一个客户端需要跟北京的一个客户端进行通信，如果按照常规路线（通过 GFW）延迟约 200ms，而如果通过云巴在美国西海岸的服务器，连接到香港、深圳的服务器，最后连到北京的这条路线，耗时约为 90ms（美国西海岸到香港）、3ms（香港到深圳）、30ms（深圳到北京）。比常规路线节省了约 80ms。

目前该项服务仅开放给付费用户。

![productpng_kb_foreign_server](https://raw.githubusercontent.com/yunba/docs/master/image/productpng_kb_foreign_server.png)

