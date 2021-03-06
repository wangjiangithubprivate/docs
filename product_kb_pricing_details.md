# 云巴产品计费规则

本文针对云巴官方网站的价格页面作补充说明。

## 计费规则

- “日活”超出当前套餐额度时，套餐会自动升级为当前“日活”所对应的套餐。
- “日活”在当前套餐额度内，但消息量或频道数量超出套餐额度时，不会升级套餐，只会加收超额部分的费用。
- “日活”低于当前套餐的额度时，会按照当前“日活”所对应的套餐来计费。
- 每 30 天生成一次账单并扣费，账单费用计算方法如下。请确保扣费前您的账户下有充足的余额。

>当月费用 = 当月订单差额 + 消息量超额费用 + 频道数量超额费用 + 预扣次月套餐费用 + 其他额外付费的服务费用

## 计费举例

### 扣费日期的计算

某用户在 2016/12/27 当天选购了某套餐并付款。30 天后，即在第 31 天（2017/1/26）时，会生成 2016/12/27 - 2017/1/25 的账单，包括当月套餐差额（多退少补），消息量、频道超出部分的费用，以及其他额外服务的费用。此外，会根据当月实际日活对应的套餐，预收次月（2017/1/26 - 2017/2/24）的套餐费用，以此类推。

### 套餐降级扣费举例

A 用户为他的应用选购了 749 元的套餐，对应为 5000 的日活、1000 万条的消息量和 7500 个频道，在第 31 天结算时，
- 实际日活为 888，在 1000 以内，则结算时会按照 249 元的套餐计费，账户结余 749 - 249 = 500 元；
- 实际消息量为 1230 万条，超出套餐 230 万条，按照每超出 100 万条需要多收 5 元计算，结算时需要另外支付 15 元；
- 实际频道数量用了 100 个，在套餐额度内，结算时不会产生额外费用；
- 另外，会按照 249 元的套餐标准收取次月的费用；

第 1 天，A 用户为他的这款应用预付了 749 元；在第 31 天发生扣款后，其账户余额为：749 - 249 - 15 - 0 - 249 = 236 元。

### 套餐升级扣费举例

B 用户也为他的某款应用选购了 749 元的套餐，对应为 5000 的日活、1000 万条的消息量和 7500 个频道，在第 31 天结算时，
- 实际日活为 5001，超过了 5000，则套餐自动升级为 1299 元的套餐，结算时需支付差额 1299 - 749 = 550 元；  
- 实际消息量为 780 万条，未超出套餐限额，不会产生额外费用；
- 实际频道数量使用了 8000 个，超出套餐 500 个，按照每超出 100 个 收 5 元计算，结算时需要额外支付 25 元；
- 另外，会按照 1299 元的套餐标准收取次月的费用；

所以，第一天，B 用户为这款应用支付了 749 元；第 31 天发生扣款后，其账户余额为：749 - 1299 - 0 - 25 - 1299 = - 1874 元。即，欠费 1874 元。


## 名词解释

- 月：按照 30 天计算。例如 用户 2016年12月27日购买套餐，其套餐扣费是从 2016年12月27日往后加 30 天来计算的。
- 日活：日活跃用户数。计算的是 30 天内，活跃用户最多的一天的活跃用户数量。活跃用户是指一段时间内的活跃用户数是指该时间段内进行过上线操作的用户数量（不一定持续在线）。
- 消息量：按云巴服务器发出的消息来计算，qos 0：算 0.5 条，qos 1、2：算 1 条。
- 权限管理：提供 App、Topic、Token 三个层级的权限控制权。详见官方文档。
- 第三方推送：集成了小米、华为推送，实现了在应用被杀的情况下，也能收到通知，引导用户打开应用。同时，支持自动创建小米、华为应用。
- 在线用户数量统计：对一段时间内持续在线的用户的数量进行统计。
- 活跃用户数量统计：对一段时间内连接过云巴服务器的用户数量（不一定持续在线）进行统计。
- 加密链接：支持 https。使用 SSL/TLS 方式进行连接，则 port 为 443；否则，port 为 3000。
- 送达确认：当第一个目标用户（且不是消息发布者）收到消息并向服务器回复了 puback 后，服务器给消息发布者发送一个 recvack。借助这个通知，消息发布者可以了解第一个收到消息的用户的 alias 和 时间戳。
- IP 固定：云巴服务的 IP 是不固定的。开通这项功能，我们可以提供 Broker 的地址和端口。
- 性能优化：包括存储优化、架构调优、网络链路优化等。
- 跨机房数据备份：按机房数量额外收费，具体内容请联系商务咨询。
- 99.999% 可用 SLA：开通“跨机房数据备份”服务，且使用三个机房或以上，即可支持此项服务，具体报价请联系商务。SLA，即 Service-level Agreement。99.999% 可用 SLA 具体的宕机时间可参考：https://uptime.is/99.999

