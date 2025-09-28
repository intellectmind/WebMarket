# WebMarket

功能强大的 Minecraft 网页市场插件，已兼容手机端显示



支持 1.20+ 的 Paper / Folia / Spigot / Bukkit / Purpur等服务端



支持 MySQL / SQLite，离线可交易，NBT 完整保存



内置 Vault 经济系统，如果有外部经济插件时启用内置经济（如cmi、ess等），此插件依然会使用内置经济处理。



你也可以禁用cmi的经济，启用此插件的经济，都是兼容的



支持混合端整合包使用（模组物品的图标资源和汉化需要自行在web目录里面添加）



内置日志系统：实时记录玩家所有关键操作（上架、购买、下架、出售、回收、登录、绑定等），方便审计与追溯



---



## 特色功能



- **离线支持**

  玩家离线时，背包数据实时入库，网页端可查看并完成上下架、购买、出售等全部操作。



- **NBT 完整**

  耐久信息、附魔、附魔书效果、药水效果、自定义名称、容器内物品的详细信息（潜影盒、收纳袋）全部保存并在网页展示。



- **容器上架**

  整盒 / 整袋一键上架，网页实时预览盒内物品。



---



## 🛒 市场系统



| 模块 | 说明 |

|---|---|

| 玩家交易市场 | 玩家自由上架、浏览、购买他人物品，支持自定义交易税费 |

| 官方商城 | 官方出售区 & 官方回收区 |

| 我的物品 | 查看 / 下架自己上架的商品 |



---



## 🎒 背包管理



- 实时网页查看在线 / 离线玩家背包

- 显示耐久、附魔、Lore、盒内物品

- 一键将背包物品直接出售到市场



---



## 🏆 排行榜



| 榜单 | 描述 |

|---|---|

| 财富榜 | 服务器最富有玩家 |

| 交易榜 | 交易量最高玩家 |

| 出售榜 | 出售最多玩家 |

| 购买榜 | 购买最多玩家 |



---



## 🔐 账户系统



- 邮箱注册 / 登录

- 游戏账号验证码绑定

- API 密钥认证 + 密码加密



---



## ⚡ 高性能



- Guava 缓存

- 全异步数据库操作

- 玩家数据实时同步



---



## 命令列表

|  命令  |  描述  |

|---|---|

| `/bind <验证码>` | 绑定网页账户到游戏账号 |

| `/claim` | 领取网页购买的物品（离线玩家或在线玩家的背包满时使用） |

| `/sell <价格> [个人限制。可选，留空或者-1表示无限制] [总数限制。可选，留空或者-1表示无限制]` | OP 专用，将手持物品上架到官方商城出售区（记录完整 NBT，包括数量所以建议手持 1 个） |

| `/recycle <价格> [个人限制。可选，留空或者-1表示无限制] [总数限制。可选，留空或者-1表示无限制]` | OP 专用，将手持物品添加到官方商城回收区（记录完整 NBT，包括数量所以建议手持 1 个） |

| `/root <邮箱>` | OP 专用，将指定邮箱用户设为管理员（可下架任何玩家物品、删除官方商城物品） |

| `/resetpassword <邮箱>` | OP 专用，重置指定邮箱用户密码，后续用户可自行在网页修改密码 |



| 内置经济系统命令 `money`也可用`bal`前缀代替 | 描述 |

|---|---|

|`/money help` | 查看WebMarket 经济系统帮助 |

|`/money` | 查看余额 |

|`/money <玩家>` | 查看其他玩家余额 |

|`/money pay <玩家> <金额> [原因]` | 转账 |

|`/money top [页码]` | 财富排行榜 |

|`/money history [玩家] [页码]` | 交易历史 |

|`/money set <玩家> <金额> [原因]` | OP 专用，设置余额 |

|`/money give <玩家> <金额> [原因]` | OP 专用，给予金钱 |

|`/money take <玩家> <金额> [原因]` | OP 专用，扣除金钱 |



---



## 权限节点



| 节点 | 用途 |

|---|---|

| `webmarket.sell` | 使用 `/sell` |

| `webmarket.recycle` | 使用 `/recycle` |

| `webmarket.root` | 使用 `/root` |

| `webmarket.resetpassword` | 使用 `/resetpassword` |



---

[SPOILER="查看可配置项config.yml"]

[CODE]

# 数据库配置

database:

  type: "SQLite" # SQLite or MySQL

  # MySQL 配置

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

  port: 8080 # 服务器监听端口

  host: "0.0.0.0" # 服务器绑定地址，"0.0.0.0" 表示监听所有网络接口



# 内置经济系统配置

simple_economy:

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

  enabled: true  # 全局玩家市场开关

  tax_rate: 0.01 # 1% 交易税率

  max_items_per_page: 30 # 每页最大商品数量

  max_listing_duration: 14 # 商品上架最大持续时间（天）

  max_listings_per_player: 10 # 每个玩家最多可上架的商品数量

  listing_cooldown_seconds: 1 # 商品上架冷却时间（秒）



# 离线背包配置

offline_inventory:

  enabled: true  # 是否启用离线背包



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

  max_price: 1000000.0



# ---------------以下一般无需修改---------------



# 日志配置

logging:

  log_market_actions: true # 是否记录市场操作

  log_auth_actions: true # 是否记录认证操作

  log_binding_actions: true # 是否记录绑定/解绑操作

  log_official_shop_actions: true # 是否记录官方商店操作

  log_password_change: true # 是否记录密码修改

  log_retention_days: 30   # 日志保留天数



# 缓存配置

cache:

  expire_after_write: 300 # 缓存写入后的过期时间（秒）

  maximum_size: 100000 # 最大缓存数量



security:

  # API密钥默认有效期（天）

  api_key_expiry_days: 7

  # 密码加密强度（迭代次数，越高越安全但越耗性能）

  encryption_iterations: 10000



# 绑定相关配置

binding:

  code_expiry_minutes: 5 # 绑定码有效期（分钟）



rate_limiting:

  # 全局API速率限制（例如：每分钟200次请求）

  global:

    requests: 100

    period: 1

    unit: MINUTES

  # 认证相关接口（登录/注册）的限流

  auth:

    requests: 5

    period: 1

    unit: MINUTES



debug:

  # 是否启用SQL查询日志（仅用于调试）

  log_sql_queries: false

  # API请求/响应日志级别

  api_log_level: "INFO" # DEBUG, INFO, WARN, ERROR

[/CODE]

[/SPOILER]

---



## 购买及激活方式



1. 前往爱发电购买

2. 运行一次插件，会生成一个`machine.txt`文件（在plugins\WebMarket\文件夹下）

3. 发送你的爱发电订单号和`machine.txt`文件到邮箱`1758426625@qq.com`获取许可证（一般最迟2天内回复）

4. 把收到的许可证放到plugins\WebMarket\文件夹内即可正常使用



---



## 购买须知



1. 插件需有效许可证，默认试用 5 分钟。购买后联系邮箱`1758426625@qq.com`获取正式许可证。

2. 许可证为离线密钥认证(安全免联网)，绑定机器。只能在一台机器上使用（如果换机器，提供相关证明，可免费发放二次许可）
