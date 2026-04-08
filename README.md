详细介绍|下载链接：https://www.minebbs.com/resources/webmarket.13231/

# WebMarket

功能强大的 Minecraft 网页市场插件，已兼容手机端显示，同步支持游戏内GUI操作

支持 1.20+ 的 Paper / Folia / Spigot / Bukkit / Purpur等服务端

支持离线操作（购买、上架、拍卖啥都行）；支持跨服，可配置按服务器隔离或全服互通

网页及游戏内GUI都支持部分ItemsAdder、CraftEngine、原版、mod等自定义物品图标显示

支持 PlayerPoints 点卷和 Vault 金币交易。玩家市场、收购、拍卖、官方商城、Buff商城、特殊物品商城都可以按金币/点卷分别定价与结算。

支持混合端整合包使用（模组物品的图标资源和汉化可能获取不全，需要自行在web目录里面添加，另附带一个exe工具，也可自动完成部分资源添加）

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

| 命令 < >必填项 [ ]可选项                                                                           | 描述                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `/wm`、`/wm gui`、`/market`                                                                  | 打开游戏内的商城 GUI。可通过权限节点 `webmarket.gui` 禁用                                                                                                                                                                                                                                                                                                                                                  |
| `/wm help`                                                                                 | 查看当前权限可使用的指令帮助                                                                                                                                                                                                                                                                                                                                                                           |
| `/wm bind <验证码>`                                                                           | 绑定网页账户到游戏账号                                                                                                                                                                                                                                                                                                                                                                              |
| `/wm register <邮箱> <密码> [用户名]`                                                             | 游戏内注册网页账号，自动绑定不可解绑。用户名可省略，默认游戏名                                                                                                                                                                                                                                                                                                                                                          |
| `/wm claim`                                                                                | 领取网页购买的物品（离线玩家或在线玩家的背包满时使用）                                                                                                                                                                                                                                                                                                                                                              |
| `/wm sj <数量> <单价> [金币/点卷]`                                                                 | 快速上架手中物品（玩家使用，可批量上架）                                                                                                                                                                                                                                                                                                                                                                     |
| `/wm sg <数量> <单价> [金币/点卷]`                                                                 | 快速收购手中物品（玩家使用）                                                                                                                                                                                                                                                                                                                                                                           |
| `/wm pm <数量> <起拍价> <时间(1-48小时)> [一口价] [金币/点卷]`                                             | 快速拍卖手中物品（玩家使用，可批量拍卖）                                                                                                                                                                                                                                                                                                                                                                     |
| `/wm sell <单价> [个人限制] [总库存] [个人限制重置周期h] [金币/点卷] [跨服/本服]`                                   | OP 专用，将手持物品上架到官方商城出售区（记录完整 NBT，包括数量所以建议手持 1 个）。默认仅限本服购买；追加 `跨服` 后才允许其他服务器购买。个人限制，留空或者-1表示无限制。总库存，留空或者-1表示无限制。个人限制重置周期，单位小时，0或留空表示不重置                                                                                                                                                                                                                                                     |
| `/wm recycle <单价> [个人限制] [总回收量] [个人限制重置周期h] [金币/点卷] [跨服/本服]`                               | OP 专用，将手持物品添加到官方商城回收区（记录完整 NBT，包括数量所以建议手持 1 个）。默认仅限本服回收；追加 `跨服` 后才允许其他服务器回收。个人限制，留空或者-1表示无限制。总回收量，留空或者-1表示无限制。个人限制重置周期，单位小时，0或留空表示不重置                                                                                                                                                                                                                                                    |
| `/wm buff <buff类型> <等级> <每秒价格> [单次最少秒数] [单次最多秒数] [个人限购秒数] [总库存秒数] [重置时间h] [金币/点卷] [跨服/本服]` | OP 专用，添加物品到官方商城Buff区。默认仅限本服购买；追加 `跨服` 后才允许其他服务器购买。可在游戏内输入/buff查看详细帮助                                                                                                                                                                                                                                                                                                                     |
| `/wm specialitem <名称> <描述> <价格> <图标材质> <指令1 指令2 ...> [个人限购] [总库存] [重置时间h] [金币/点卷] [跨服/本服]` | OP 专用，添加物品到官方商城特殊物品区。默认仅限本服购买；追加 `跨服` 后才允许其他服务器购买。支持变量{player}，多条指令以竖线相隔。可在游戏内输入/specialitem查看详细帮助                                                                                                                                                                                                                                                                                       |
| `/wm root <邮箱>`                                                                            | OP 专用，将指定邮箱用户设为管理员（可下架任何玩家物品、删除官方商城物品）                                                                                                                                                                                                                                                                                                                                                   |
| `/wm unroot <邮箱>`                                                                          | OP 专用，取消指定邮箱用户管理员                                                                                                                                                                                                                                                                                                                                                                        |
| `/wm resetpassword <邮箱>`                                                                   | OP 专用，重置指定邮箱用户密码，后续用户可自行在网页修改密码                                                                                                                                                                                                                                                                                                                                                          |
| `/wm marketlogs me`                                                                        | 查询自己的交易记录。筛选条件: -type:类型参数（buy: 所有购买记录（玩家市场购买 + 官方商城购买 + 收购创建） sell:所有出售记录（官方商城回收 + 满足收购） list: 玩家市场上架记录 delist: 玩家市场下架记录 auction: 拍卖记录 request: 收购相关记录（创建/撤销/过期） buff: Buff购买记录 special: 特殊物品购买记录 shop: 所有商城购买记录 all: 所有记录）、-time:时间参数（today: 今天 yesterday: 昨天 week: 最近7天 month: 最近30天 custom:yyyy-MM-dd: 从指定日期开始 custom:yyyy-MM-dd:yyyy-MM-dd: 指定日期范围）。                                |
| `/wm marketlogs <玩家名> [页码] [筛选条件]`                                                         | OP 专用，查询指定玩家的交易记录。筛选条件: -type:类型参数（buy: 所有购买记录（玩家市场购买 + 官方商城购买 + 收购创建） sell:所有出售记录（官方商城回收 + 满足收购） list: 玩家市场上架记录 delist: 玩家市场下架记录 auction: 拍卖记录 request: 收购相关记录（创建/撤销/过期） buff: Buff购买记录 special: 特殊物品购买记录 shop: 所有商城购买记录 all: 所有记录）、-time:时间参数（today: 今天 yesterday: 昨天 week: 最近7天 month: 最近30天 custom:yyyy-MM-dd: 从指定日期开始 custom:yyyy-MM-dd:yyyy-MM-dd: 指定日期范围）。可在游戏内输入/marketlogs打开GUI |
| `/wm marketlogs-material <物品材质> [页码] [筛选条件]`                                               | OP 专用，查询指定物品的交易记录。筛选条件: -type:类型参数（market: 玩家市场记录 auction: 拍卖记录 buy_request: 收购记录 official_buy: 官方购买 official_sell: 官方回收 all: 所有记录）、-time:时间参数（today: 今天 yesterday: 昨天 week: 最近7天 month: 最近30天 custom:yyyy-MM-dd: 从指定日期开始 custom:yyyy-MM-dd:yyyy-MM-dd: 指定日期范围）。可在游戏内输入/marketlogs-material打开GUI                                                                                         |
| `/wm restrict`                                                                             | OP 专用，可分别限制某个玩家使用市场上架、收购或者拍卖创建功能。可在游戏内输入/restrict查看详细帮助                                                                                                                                                                                                                                                                                                                                  |
| `/wm blockitem`                                                                            | OP 专用，禁止手上的物品上架、创建收购、拍卖，以防止某些菜单道具被上架。可在游戏内输入/blockitem查看详细帮助                                                                                                                                                                                                                                                                                                                             |
| `/wm iconcache`                                                                            | OP 专用，管理 WebMarket 自动生成的网页图标缓存，包括查看缓存状态、清空缓存、清理过期缓存。 |

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
| `webmarket.blockitem` | 使用 `/iconcache` |
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

---

## 配置文件

```yaml
activation_code: "" # 激活码

# 插件语言配置
# 可选值: zh_cn, en_us
language: "zh_cn"

# 数据库配置
database:
  type: "SQLite" # SQLite or MySQL
  # MySQL 配置（人多使用这个数据库，需8.0+）
  host: "localhost"
  port: 3306
  database: "webmarket"
  username: "root"
  password: ""
  # 连接池设置
  pool:
    max_size: 10
    min_idle: 2
    connection_timeout: 30000
    idle_timeout: 600000
    max_lifetime: 1800000
    leak_detection_threshold: 60000

# API 服务器配置
api:
  enabled: true # 是否启用 HTTP API / Web 服务
  enable_on_secondary_shared_server: false # shared 模式下副服务器是否也启动 HTTP 服务；通常只需主服务器开启
  port: 8880 # 服务器监听端口
  host: "0.0.0.0" # 服务器绑定地址，"0.0.0.0" 表示监听所有网络接口
  worker_threads: 4 # API请求处理线程数
  queue_capacity: 1600 # 请求队列容量
  ssl:
    enabled: false # 是否启用 HTTPS。关闭时使用普通 HTTP
    key_store_path: "ssl/keystore.p12" # 证书库路径。可填绝对路径，或相对 plugins/WebMarket/ 的路径
    key_store_password: "" # 证书库密码
    key_password: "" # 私钥密码。留空时默认使用 key_store_password
    key_store_type: "PKCS12" # 证书库类型，例如 PKCS12 / JKS
    protocol: "TLS" # SSLContext 协议，一般保持 TLS 即可

# 玩家身份（绑定）匹配模式
player_identity:
  mode: "uuid" # uuid=按UUID识别（在线服推荐），name=按游戏名识别（离线服推荐）

# Web 前端配置
# 如需自定义标签logo图标 图片可放在 plugins/WebMarket/web-assets/logo/logo.png
web:
  # 网站Logo文字
  logo_text: 'WebMarket'
  # 是否优先使用自定义名称图片资源。可放在 plugins/WebMarket/web-assets/custom-images/<自定义名称>.png 不需要带颜色格式符
  # 启用后会优先获取自定义命名的图片资源，找不到则会回退到显示为物品材质图片（排除玩家自主命名的）
  use_custom_name_image: true
  # 是否允许自定义名称覆盖物品材质名称，启用后优先显示自定义名称，不再显示“自定义名称”行（排除玩家自主命名的）
  use_custom_name_override: true
  # 是否启用后端生成并缓存网页物品图标。生成结果会保存到 plugins/WebMarket/web-assets/generated-icons/
  generated_item_icons:
    enabled: true
    # 注意：开启后，会导致你的 CraftEngine/ItemsAdder 等自定义的图标资源泄露
    # 是否允许为 ItemsAdder 自定义物品生成网页图标
    itemsadder_enabled: false
    # 是否允许为 CraftEngine 自定义物品生成网页图标
    craftengine_enabled: false
    # 是否允许从服务端原版资源中提取网页图标
    vanilla_enabled: true
    # 当本地找不到原版资源时，是否尝试从官方 Minecraft 客户端资源下载并缓存
    vanilla_download_enabled: true
    # 原版客户端下载源列表。按顺序尝试，官方源会作为最后回退。
    # 每个源填写一个基础地址，程序会自动拼接 Mojang/Piston 路径。
    vanilla_download_sources:
      - "https://bmclapi2.bangbang93.com"
      - "https://launchermeta.mojang.com"
    # 是否允许从世界 datapacks 中提取网页图标和模型覆盖
    datapack_enabled: true
    # 是否允许从混合端 mods 资源中提取网页图标
    hybrid_mod_enabled: true
    # 是否输出 CE/IA/资源命中相关调试日志
    debug_logging: false
    # 是否启用图标缓存文件自动清理
    cleanup_enabled: true
    # generated-icons 目录中文件的最大保留天数，0 表示关闭该目录自动清理
    generated_icons_max_age_days: 0
    # vanilla-cache 目录中文件的最大保留天数，0 表示关闭该目录自动清理
    vanilla_cache_max_age_days: 30

# 跨服配置
cross_server:
  enabled: false # 是否启用跨服支持（仅 MySQL 可用，SQLite 下会自动禁用）
  mode: "isolated" # isolated=按服务器隔离（仅聚合商品）, shared=全服互通
  server_name: "server-1" # 当前服务器唯一名称
  server_aliases: [] # 旧服务器名称别名列表。改过 server_name 时可填写旧名字，兼容旧离线背包和旧 server_name 记录
  master_server_name: "server-1" # 主服务器名称
  item_sync_enabled: false # 是否已安装跨服物品同步方案。开启后将停用插件自带的离线背包快照机制：不再保存/恢复离线背包，并禁止玩家离线时进行需要直接扣除背包物品的操作（如市场上架、创建拍卖、卖给收购、官方商店回收）
  economy_sync_enabled: false # 经济余额是否跨服共享。isolated 模式下设为 false 时，金币余额与财富排行榜会按服务器独立存储和统计；点卷直接读取本服 PlayerPoints，不受此配置控制
  transaction_sync_enabled: false # 交易统计是否跨服共享。isolated 模式下设为 false 时，排行榜的交易/出售/购买统计会按服务器隔离
  known_servers: # 前端/GUI 可选择的服务器列表
    - "server-1"

# 内置经济系统配置
simple_economy:
  # 跨服建议优先使用内置经济
  # 是否启用内置Vault经济系统（没有外部经济插件时使用，如cmi、ess等）
  # 如果有外部经济插件时启用此项，此插件依然会使用内置经济处理
  # 你也可以禁用cmi的经济，启用此插件的经济，都是兼容的
  enabled: false
  starting_balance: 100.0  # 新玩家初始余额
  max_balance: 999999999.0  # 最大余额限制
  min_transfer: 0.01  # 最小转账金额
  currency_singular: "金币"  # 货币单数名称
  currency_plural: "金币"    # 货币复数名称
  # 交易记录保留天数（-1为永久保留）
  transaction_history_days: 30

# 市场设置
market:
  enabled: true # 全局玩家市场开关
  tax_payer: "seller" # 税费承担方：seller=卖家承担（买家按报价支付），buyer=买家承担（买家按报价+税支付）
  tax_rates:
    money: 0.01 # 金币交易税率
    points: 0.00 # 点卷交易税率（点卷按整数结算，非0税率会四舍五入到整数税额）
  max_items_per_page: 24 # 每次慢加载的商品数量
  max_listing_duration: 14 # 商品上架最大持续时间（天）
  max_listings_per_player: 10 # 每个玩家最多可上架的商品数量
  listing_cooldown_seconds: 1 # 商品上架冷却时间（秒）
  # 物品上架限制
  item_restrictions:
    # 物品限制模式:
    # - "none": 无限制（默认）
    # - "whitelist": 仅允许列表中的物品上架
    # - "blacklist": 禁止列表中的物品上架
    mode: "none"
    # 限制列表（根据mode决定是白名单还是黑名单）
    items:
      # 物品ID（格式：minecraft:item_id 或直接写 ITEM_ID）
      - "minecraft:bedrock"
      - "minecraft:command_block"
  # 收购功能配置
  buy_request:
    enabled: true # 是否启用收购功能
    tax_payer: "seller" # 税费承担方：seller=卖家承担（卖家到账=报价-税），buyer=买家承担（卖家按报价到账）
    tax_rates:
      money: 0.02 # 金币收购成交税率
      points: 0.00 # 点卷收购成交税率（卷按整数结算，税费会取整）
    max_quantity: 99999 # 单笔收购允许创建的最大数量
    max_requests_per_player: 3 # 每个玩家最多可发布的收购数量
    max_request_duration: 7 # 收购最大持续时间（天）
    request_cooldown_seconds: 1 # 发布收购冷却时间（秒）
    # 收购物品限制
    item_restrictions:
      mode: "none" # none, whitelist, blacklist
      # 限制列表（根据mode决定是白名单还是黑名单）
      items:
        - "minecraft:bedrock"
        - "minecraft:command_block"

# 拍卖行配置
auction:
  enabled: true # 全局拍卖行开关
  tax_payer: "seller" # 税费承担方：seller=卖家承担（买家按报价支付），buyer=买家承担（买家按报价+税支付）
  tax_rates:
    money: 0.03 # 金币拍卖税率
    points: 0.00 # 点卷拍卖税率（点卷按整数结算，税费会取整）
  max_items_per_page: 24 # 每次慢加载的商品数量
  max_listings_per_player: 10 # 每个玩家最多同时拍卖的数量
  listing_cooldown_seconds: 1 # 上架冷却时间 (秒)
  max_duration_hours: 48 # 最大拍卖持续时间（小时）
  # 拍卖上架限制
  item_restrictions:
    mode: "none" # none, whitelist, blacklist
    # 限制列表（根据mode决定是白名单还是黑名单）
    items:
      # 物品ID（格式：minecraft:item_id 或直接写 ITEM_ID）
      - "minecraft:bedrock"
      - "minecraft:command_block"

# 离线背包配置
offline_inventory:
  enabled: true  # 是否启用离线背包

# 官方商店配置
official_shop:
  # 动态定价系统配置
  dynamic_pricing:
    # 是否启用动态定价系统
    # 使用3天加权平均和sigmoid函数平滑变化
    # 动态价格 = 原价 × (1 + sigmoid(3天趋势) × 敏感度 × 趋势权重)
    enabled: true

    # 价格重置策略
    # false: 不重置（价格会持续根据交易量变化）
    # daily: 每日重置（每天00:00后首次检查时重置为原价）
    # weekly: 每周重置（每周一重置为原价）
    # monthly: 每月重置（每月1号重置为原价）
    restart: false

    # 交易活跃度算法配置
    activity:
      # 敏感度 (0.01-1.0)
      # 值越高，交易量变化对价格影响越大
      # 推荐值：0.05-0.2
      sensitivity: 0.1

      # 每日交易量阈值
      # 今日交易量达到此值才开始计算价格波动
      # 避免少量交易造成剧烈波动，建议设为1-10
      daily_volume_threshold: 1

    # 全局价格保护（最终价格限制）
    price_protection:
      # 是否启用价格下限
      enable_floor: true

      # 最低价格倍数 (相对于原价)
      # 算法会根据价格波动率动态调整：
      # - 高波动(>30%): 限制为原价的0.7-1.5倍
      # - 中波动(>10%): 限制为原价的0.5-2.0倍
      # - 低波动: 使用配置的倍数值
      min_price_multiplier: 0.5

      # 是否启用价格上限
      enable_ceiling: true

      # 最高价格倍数 (相对于原价)
      # 同样会根据波动率动态调整
      max_price_multiplier: 2.0

# 物品相关配置
items:
  # 物品最大堆叠数量检查
  max_stack_size_check: true
  # 允许单次上架的最小数量
  min_quantity: 1
  # 允许单次上架的最大数量
  max_quantity: 2304
  # 价格限制
  min_price: 0.01
  max_price: 10000000.0

security:
  # API密钥默认有效期（天）
  api_key_expiry_days: 7
  # 密码加密强度（迭代次数，越高越安全但越耗性能）
  encryption_iterations: 10000
  # 是否启用邮箱白名单（启用后仅允许白名单域名注册）
  email_whitelist_enabled: false
  # 邮箱域名白名单（仅填写域名，不带@）
  # 示例: ["qq.com", "gmail.com"]
  email_whitelist_domains:
    - "qq.com"
  # 同IP注册限制（每个IP最多可注册的账户数量，0为无限制）
  registration_limit_per_ip: 2
  # 是否允许通过 Web 表单注册（关闭后仅允许通过 AuthMe 注册并登录）
  allow_web_registration: true

# AuthMe
authme_login:
  # 是否启用 AuthMe 登录（游戏名、邮箱都可登录。不可解绑账号）
  enabled: false
  # 当 AuthMe 未注册邮箱时使用的邮箱域名（最终邮箱: <游戏名>@<域名>）
  fallback_email_domain: "authme.local"
  # 外部 AuthMe 数据库（代理服/登录服的 AuthMe 不在本服时使用）
  # 启用后无需本服安装 AuthMe 插件，直接连接远程 AuthMe 数据库进行认证
  # 仅支持 MySQL/MariaDB；密码算法支持 SHA256（AuthMe 默认）和 bcrypt
  external_database:
    enabled: false
    host: "localhost"
    port: 3306
    database: "authme"
    username: "root"
    password: ""
    table_name: "authme"          # AuthMe 数据表名
    password_column: "password"   # 密码列名
    username_column: "username"   # 用户名列名
    email_column: "email"         # 邮箱列名

# ---------------以下一般无需修改---------------

# 日志配置
logging:
  log_market_actions: true # 是否记录市场操作
  log_auth_actions: true # 是否记录认证操作
  log_binding_actions: true # 是否记录绑定/解绑操作
  log_official_shop_actions: true # 是否记录官方商店操作
  log_password_change: true # 是否记录密码修改
  log_auction_actions: true # 是否记录拍卖操作
  log_buy_request_actions: true  # 是否记录求购操作
  log_retention_days: 30   # 日志保留天数

# 缓存配置
cache:
  expire_after_write: 300 # 缓存写入后的过期时间（秒）
  maximum_size: 100000 # 最大缓存数量

# 排行榜配置
leaderboard:
  fetch_interval_minutes: 10 # 排行榜数据缓存/刷新间隔（分钟）。在间隔内重复请求会直接返回缓存结果

# PlaceholderAPI 配置
placeholderapi:
  wealth_cache_seconds: 10 # 财富榜占位符缓存时间（秒），0 表示不保留缓存、每次请求触发异步刷新

# 绑定相关配置
binding:
  code_expiry_minutes: 5 # 绑定码有效期（分钟）

rate_limiting:
  # 全局API速率限制（例如：每分钟100次请求）
  global:
    requests: 100
    period: 1
    unit: MINUTES
  # 认证相关接口（登录/注册）的限流
  auth:
    requests: 5
    period: 1
    unit: MINUTES

license:
  cloud:
    # 是否忽略HTTPS证书校验
    ignore_ssl_errors: true

# 更新检查配置
update_checker:
  # 是否启用更新检查
  enabled: true
  # 检查间隔（小时）
  check_interval_hours: 48
  # 是否在玩家进入时通知管理员有更新
  notify_admins_on_join: true

debug:
  # 是否启用SQL查询日志（仅用于调试）
  log_sql_queries: false
  # API请求/响应日志级别
  api_log_level: "INFO" # DEBUG, INFO, WARN, ERROR
```
