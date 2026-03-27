详细介绍|下载链接：https://www.minebbs.com/resources/webmarket.13231/

# WebMarket

功能强大的 Minecraft 网页市场插件，已兼容手机端显示，同步支持游戏内GUI操作

支持 1.20+ 的 Paper / Folia / Spigot / Bukkit / Purpur等服务端

支持离线操作（购买、上架、拍卖啥都行）

支持跨服，可配置按服务器隔离或全服互通

支持 PlayerPoints 点卷和 Vault 金币交易。玩家市场、收购、拍卖、官方商城、Buff商城、特殊物品商城都可以按金币/点卷分别定价与结算。

支持混合端整合包使用（模组物品的图标资源和汉化需要自行在web目录里面添加，附带一个exe工具，可自动完成部分资源添加）

---

## 特色功能

- **离线支持**

  玩家离线时，背包数据实时入库，网页端可查看并完成上下架、购买、出售等全部操作。

- **NBT 完整**

  耐久信息、附魔、附魔书效果、药水效果、自定义名称、容器内物品的详细信息（潜影盒、收纳袋）全部保存并在网页展示。支持优先获取自定义命名的图片资源，找不到则会回退到显示为物品材质图片（会自动排除玩家命名的物品）。

- **容器上架**

  整盒 / 整袋一键上架，网页实时预览盒内物品，游戏内GUI也同步支持预览容器。

- **官方商城动态定价**

  计算公式：动态价格 = 原价 × (1 + sigmoid(3天趋势) × 敏感度 × 趋势权重)

- **Buff商城+特殊物品/权益区**

  Buff商城可按秒购买Buff，需要玩家在线。

  特殊物品/权益区，购买后执行自定义一条或多条指令，支持变量{player}，方便购买权益。

  特殊物品创建后，拥有管理员权限的账号可直接在网页修改所有信息。

- **市场收购**

  可通过以下两种方式：

  ①通过手持物品指令/sg <数量> <单价>创建收购，可记录完整nbt数据（推荐）

  ②直接在网页创建收购，缺点：只能创建基础属性物品（不含附魔、药水、lore信息等）

---

## 🛒 市场系统

| 模块 | 说明 |
|---|---|
| 玩家交易市场 | 玩家自由上架、收购、购买他人物品，支持自定义交易税费，支持白名单、黑名单模式 |
| 拍卖行 | 拍卖区域，支持自定义交易税费，支持白名单、黑名单模式 |
| 官方商城 | 官方出售区 & 官方回收区 & Buff区 & 特殊物品区，官方出售+回收区可启用动态定价系统 |

---

## 🎒 背包管理

- 实时网页查看在线 / 离线玩家背包

- 显示耐久、附魔、Lore、盒内物品

- 一键将背包物品直接出售到市场、拍卖行

---

## 🏆 排行榜

| 榜单 | 描述 |
|---|---|
| 财富榜 | 服务器最富有玩家 |
| 交易榜 | 交易最高玩家 |
| 出售榜 | 出售最多玩家 |
| 购买榜 | 购买最多玩家 |

---

## 🔐 账户系统

- 支持AuthMe，可通过游戏名或邮箱登录。登录后自动绑定账号，不可解绑

- 游戏内可通过 `/wm register <邮箱> <密码> [用户名]` 注册网页账号，自动绑定不可解绑。用户名可省略，默认游戏名

- Web页面邮箱注册，需手动绑定游戏账号，可解绑

- API 密钥免认证登录

---

## 命令列表

所有命令都以 `/wm` 开头，你也可以省略前面的 `/wm` 使用简写命令。

| 命令 < >必填项 [ ]可选项                                                                         | 描述                                                                                                                                                                                                                                                                                                                                                                                       |
|------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `/wm gui` 或 `/market`| 打开游戏内的商城 GUI。可通过权限节点 `webmarket.gui` 禁用                                                                                                                                                                                                                                                                                                                                                  |
| `/wm` 或 `/wm help`| 查看当前权限可使用的指令帮助                                                                                                                                                                                                                                                                                                                                                                           |
| `/wm bind <验证码>`| 绑定网页账户到游戏账号                                                                                                                                                                                                                                                                                                                                                                              |
| `/wm register <邮箱> <密码> [用户名]`| 游戏内注册网页账号，自动绑定不可解绑。用户名可省略，默认游戏名                                                                                                                                                                                                                                                                                                                                                          |
| `/wm claim`| 领取网页购买的物品（离线玩家或在线玩家的背包满时使用）                                                                                                                                                                                                                                                                                                                                                              |
| `/wm sj <数量> <单价> [金币/点卷]`| 快速上架手中物品（玩家使用，可批量上架）                                                                                                                                                                                                                                                                                                                                                                     |
| `/wm sg <数量> <单价> [金币/点卷]`| 快速收购手中物品（玩家使用）                                                                                                                                                                                                                                                                                                                                                                           |
| `/wm pm <数量> <起拍价> <时间(1-48小时)> [一口价] [金币/点卷]`| 快速拍卖手中物品（玩家使用，可批量拍卖）                                                                                                                                                                                                                                                                                                                                                                     |
| `/wm sell <单价> [个人限制] [总库存] [个人限制重置周期h] [金币/点卷] [跨服/本服]`| OP 专用，将手持物品上架到官方商城出售区（记录完整 NBT，包括数量所以建议手持 1 个）。默认仅限本服购买；追加 `跨服` 后才允许其他服务器购买。个人限制，留空或者-1表示无限制。总库存，留空或者-1表示无限制。个人限制重置周期，单位小时，0或留空表示不重置                                                                                                                                                                                                                                                     |
| `/wm recycle <单价> [个人限制] [总回收量] [个人限制重置周期h] [金币/点卷] [跨服/本服]`| OP 专用，将手持物品添加到官方商城回收区（记录完整 NBT，包括数量所以建议手持 1 个）。默认仅限本服回收；追加 `跨服` 后才允许其他服务器回收。个人限制，留空或者-1表示无限制。总回收量，留空或者-1表示无限制。个人限制重置周期，单位小时，0或留空表示不重置                                                                                                                                                                                                                                                    |
| `/wm buff <buff类型> <等级> <每秒价格> [单次最少秒数] [单次最多秒数] [个人限购秒数] [总库存秒数] [重置时间h] [金币/点卷] [跨服/本服]`| OP 专用，添加物品到官方商城Buff区。默认仅限本服购买；追加 `跨服` 后才允许其他服务器购买。可在游戏内输入/buff查看详细帮助                                                                                                                                                                                                                                                                                                                     |
| `/wm specialitem <名称> <描述> <价格> <图标材质> <指令1 指令2 ...> [个人限购] [总库存] [重置时间h] [金币/点卷] [跨服/本服]`| OP 专用，添加物品到官方商城特殊物品区。默认仅限本服购买；追加 `跨服` 后才允许其他服务器购买。支持变量{player}，多条指令以竖线相隔。可在游戏内输入/specialitem查看详细帮助                                                                                                                                                                                                                                                                                       |
| `/wm root <邮箱>`| OP 专用，将指定邮箱用户设为管理员（可下架任何玩家物品、删除官方商城物品）                                                                                                                                                                                                                                                                                                                                                   |
| `/wm unroot <邮箱>`| OP 专用，取消指定邮箱用户管理员                                                                                                                                                                                                                                                                                                                                                                        |
| `/wm resetpassword <邮箱>`| OP 专用，重置指定邮箱用户密码，后续用户可自行在网页修改密码                                                                                                                                                                                                                                                                                                                                                          |
| `/wm marketlogs me`| 查询自己的交易记录。筛选条件: -type:类型参数（buy: 所有购买记录（玩家市场购买 + 官方商城购买 + 收购创建） sell:所有出售记录（官方商城回收 + 满足收购） list: 玩家市场上架记录 delist: 玩家市场下架记录 auction: 拍卖记录 request: 收购相关记录（创建/撤销/过期） buff: Buff购买记录 special: 特殊物品购买记录 shop: 所有商城购买记录 all: 所有记录）、-time:时间参数（today: 今天 yesterday: 昨天 week: 最近7天 month: 最近30天 custom:yyyy-MM-dd: 从指定日期开始 custom:yyyy-MM-dd:yyyy-MM-dd: 指定日期范围）。                                |
| `/wm marketlogs <玩家名> [页码] [筛选条件]`| OP 专用，查询指定玩家的交易记录。筛选条件: -type:类型参数（buy: 所有购买记录（玩家市场购买 + 官方商城购买 + 收购创建） sell:所有出售记录（官方商城回收 + 满足收购） list: 玩家市场上架记录 delist: 玩家市场下架记录 auction: 拍卖记录 request: 收购相关记录（创建/撤销/过期） buff: Buff购买记录 special: 特殊物品购买记录 shop: 所有商城购买记录 all: 所有记录）、-time:时间参数（today: 今天 yesterday: 昨天 week: 最近7天 month: 最近30天 custom:yyyy-MM-dd: 从指定日期开始 custom:yyyy-MM-dd:yyyy-MM-dd: 指定日期范围）。可在游戏内输入/marketlogs打开GUI |
| `/wm marketlogs-material <物品材质> [页码] [筛选条件]`| OP 专用，查询指定物品的交易记录。筛选条件: -type:类型参数（market: 玩家市场记录 auction: 拍卖记录 buy_request: 收购记录 official_buy: 官方购买 official_sell: 官方回收 all: 所有记录）、-time:时间参数（today: 今天 yesterday: 昨天 week: 最近7天 month: 最近30天 custom:yyyy-MM-dd: 从指定日期开始 custom:yyyy-MM-dd:yyyy-MM-dd: 指定日期范围）。可在游戏内输入/marketlogs-material打开GUI|
| `/wm restrict`| OP 专用，可分别限制某个玩家使用市场上架、收购或者拍卖创建功能。可在游戏内输入/restrict查看详细帮助                                                                                                                                                                                                                                                                                                                                  |
| `/wm blockitem`| OP 专用，禁止手上的物品上架、创建收购、拍卖，以防止某些菜单道具被上架。可在游戏内输入/blockitem查看详细帮助                                                                                                                                                                                                                                                                                                                             |

| 内置经济系统命令 `/wm money` 也可用 `/wm bal` 前缀代替 | 描述 |
|---|---|
|`/wm money help` | 查看WebMarket 经济系统帮助 |
|`/wm money` | 查看余额 |
|`/wm money <玩家>` | 查看其他玩家余额 |
|`/wm money pay <玩家> <金额> [原因]` | 转账 |
|`/wm money top [页码]` | 财富排行榜 |
|`/wm money history [玩家] [页码]` | 交易历史 |
|`/wm money set <玩家> <金额> [原因]` | OP 专用，设置余额 |
|`/wm money give <玩家> <金额> [原因]` | OP 专用，给予金钱 |
|`/wm money take <玩家> <金额> [原因]` | OP 专用，扣除金钱 |

---

## 权限节点

| 节点 | 用途 |
|---|---|
| `webmarket.sell` | 使用 `/sell` |
| `webmarket.recycle` | 使用 `/recycle` |
| `webmarket.root` | 使用 `/root` 和 `/unroot` |
| `webmarket.resetpassword` | 使用 `/resetpassword` |
| `webmarket.marketlogs` | 使用 `/marketlogs` 与 `/marketlogs-material` |
| `webmarket.marketlogs.self` | 查询自己的交易记录（`/marketlogs me` 或不带参数打开 GUI） |
| `webmarket.restrict` | 使用 `/restrict` |
| `webmarket.buff` | 使用 `/buff` |
| `webmarket.specialitem` | 使用 `/specialitem` |
| `webmarket.blockitem` | 使用 `/blockitem` |
| `webmarket.gui` | 使用 `/wm gui` |
| `webmarket.use` | 部分基础命令权限 |
| `webmarket.publish.points` | 允许发布点卷商品/点卷收购/点卷拍卖。未安装 LuckPerms 时默认开放；安装后由权限插件接管 |
| `webmarket.money.balance` | 查看自己的余额 |
| `webmarket.money.others` | 查看其他玩家余额 |
| `webmarket.money.pay` | 转账给其他玩家 |
| `webmarket.money.top` | 查看财富排行榜 |
| `webmarket.money.history` | 查看自己的交易记录 |
| `webmarket.money.history.others` | 查看其他玩家交易记录 |
| `webmarket.money.admin` | 管理员经济命令（设置/给予/扣除） |

---

## PlaceholderAPI 占位符

安装 `PlaceholderAPI` 后，插件会自动注册 `%webmarket_*%` 占位符。

当前已支持以下财富/余额相关占位符：

| 占位符 | 说明 |
|---|---|
| `%webmarket_balance%` | 当前玩家金币余额，纯数字格式 |
| `%webmarket_balance_formatted%` | 当前玩家金币余额，使用经济系统格式化后的显示文本 |
| `%webmarket_rank%` | 当前玩家在财富榜中的名次，未上榜返回 `0` |
| `%webmarket_top_1_name%` | 财富榜第 1 名玩家名称 |
| `%webmarket_top_1_player%` | 同 `%webmarket_top_1_name%` |
| `%webmarket_top_1_balance%` | 财富榜第 1 名玩家余额，纯数字格式 |
| `%webmarket_top_1_balance_formatted%` | 财富榜第 1 名玩家余额，格式化显示 |
| `%webmarket_top_1_rank%` | 返回对应名次本身，例如第 1 名返回 `1` |

说明：

- 上面的 `1` 可以替换成任意名次，例如 `%webmarket_top_5_name%`、`%webmarket_top_10_balance%`
- 当前占位符默认基于金币财富榜，不包含点卷榜
- 为避免记分板频繁刷新时反复扫库，财富榜占位符使用缓存，缓存时间配置项为 `placeholderapi.wealth_cache_seconds`，默认 `60` 秒；配置为 `0` 时不保留缓存，每次请求都会触发一次异步刷新

---

## 玩家个性化配置（权限组支持）

通过权限组可为玩家单独设置上架数量、税率、有效天数等参数：

### 出售系统

- `webmarket.limit.market.sell.max_listings.<数值>`

  最大上架数量

- `webmarket.limit.market.sell.max_duration_days.<天数>`

  最大持续天数

- `webmarket.tax.market.sell.money.<税率>`

  金币出售税率

- `webmarket.tax.market.sell.points.<税率>`

  点卷出售税率

### 收购系统

- `webmarket.limit.market.buy.max_requests.<数值>`

  最大收购数量

- `webmarket.limit.market.buy.max_duration_days.<天数>`

  最大持续天数

- `webmarket.tax.market.buy.money.<税率>`

  金币收购税率

- `webmarket.tax.market.buy.points.<税率>`

  点卷收购税率

### 拍卖行

- `webmarket.limit.auction.max_listings.<数值>`

  最大拍卖数量

- `webmarket.limit.auction.max_duration_hours.<小时>`

  最大拍卖持续时间（小时）

- `webmarket.tax.auction.money.<税率>`

  金币拍卖税率

- `webmarket.tax.auction.points.<税率>`

  点卷拍卖税率

---

## 跨服配置

在 `config.yml` 中可通过 `cross_server` 控制跨服行为：

- 跨服功能仅支持 **MySQL**。如果 `database.type` 不是 `MySQL`，即使 `cross_server.enabled: true` 也会在运行时自动禁用。

- `cross_server.mode`: `isolated` 为各服市场/拍卖数据隔离；`shared` 为市场/拍卖互通，成交物品进入待领取区。
- `cross_server.server_name`: 当前服务器唯一标识。
- `cross_server.server_aliases`: 当前服务器的旧名称列表。修改过 `server_name` 后，可把旧名字填在这里，兼容旧离线背包键和旧 `server_name` 数据。
- `cross_server.master_server_name`: `shared` 模式下主服务器名称，市场/拍卖相关配置从主服同步。
- `cross_server.item_sync_enabled`: 是否启用外部跨服物品同步。关闭时插件会自己维护按服务器隔离的离线背包；开启时，插件会停止依赖自己的离线背包快照，并禁止部分玩家离线时的物品操作，避免和外部同步方案打架。
- `cross_server.known_servers`: 已知服务器列表，用于网页和 GUI 的服务器筛选项。
- 启用跨服后，动态价格重置/每日刷新等部分全局任务仅由 `master_server_name` 对应服务器执行，避免多服重复更新。

---

## 购买及激活方式

1. 前往爱发电购买

2. 发送你的爱发电订单号到QQ`1758426625` 或者邮箱`1758426625@qq.com`获取激活码

3. 把激活码填写到配置文件中的`activation_code`即可正常使用

---

## 购买须知

1. 插件使用需激活码，每个激活码同时仅限1个IP地址使用。

2. 如更换IP后显示激活失败，请等待至少40分钟后再次尝试。

3. 如果您的激活码被滥用，开发者有权禁用您的激活码。

---

## bStats

![bStats](https://bstats.org/signatures/bukkit/webmarket.svg)
