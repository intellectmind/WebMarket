# WebMarket Free

[演示视频](https://www.bilibili.com/video/BV1fUD7BgEtL/) /
[演示站点](https://sd.kurt6.cn)

支持 `1.20+` 的 Paper / Folia / Spigot / Bukkit / Purpur 服务端，网页端兼容手机与桌面浏览器。

免费版聚焦基础网页市场、背包查看、待领取、交易日志、账号系统与经济能力。

---

## 功能范围

- 基础玩家市场
  支持玩家上架、购买、下架物品，免费版运行时最多同时上架 `100` 个玩家市场物品。

- 离线操作
  玩家离线时仍可通过网页查看背包/末影箱，处理待领取物品，完成基础市场相关操作。

- 完整物品信息展示
  支持显示耐久、附魔、Lore、自定义名称、药水效果、潜影盒/收纳袋内容等 NBT 信息。

- 交易日志
  支持查询玩家交易记录、物品材质交易记录。

- 账户系统
  支持网页注册、游戏内注册、账号绑定、密码修改、API Key 免登录。

- 内置经济与 Vault 经济
  支持金币交易、转账、余额查询、财富排行榜、交易历史。

- 图标与资源回退
  支持原版、部分自定义物品资源与自动图标缓存生成。

---

## 免费版不包含

- 游戏内 GUI
- 收购系统
- 拍卖行
- 官方商城出售 / 回收
- Buff 商城
- 特殊物品 / 权益区
- 跨服功能
- 远程背包操作
- 点卷交易
- 玩家个性化配置（权限组支持）

---

## 安装

1. 将免费版 jar 放入服务器 `plugins` 目录。
2. 启动服务器生成配置文件。
3. 按需修改 `config.yml` 或 `config.en_us.yml`。
4. 重启服务器。

---

## 主要命令

所有命令都支持 `/wm` 前缀，部分也有短命令别名。

| 命令 | 说明 |
|---|---|
| `/wm help` | 查看当前可用帮助 |
| `/wm bind <验证码>` | 绑定网页账号到游戏账号 |
| `/wm register <邮箱> <密码> [用户名]` | 在游戏内注册网页账号 |
| `/wm claim` | 领取待领取物品 |
| `/wm sj <数量> <单价>` | 快速上架手中物品到玩家市场 |
| `/wm marketlogs me` | 查询自己的交易记录 |
| `/wm marketlogs <玩家> [页码] [筛选条件]` | 管理员查询指定玩家交易记录 |
| `/wm marketlogs-material <物品材质> [页码] [筛选条件]` | 查询指定材质交易记录 |
| `/wm restrict` | 管理基础玩家市场上架限制 |
| `/wm blockitem` | 管理禁止上架的 NBT 物品 |
| `/wm money` | 查看余额 |
| `/wm money pay <玩家> <金额> [原因]` | 金币转账 |
| `/wm money top [页码]` | 财富排行榜 |
| `/wm money history [玩家] [页码]` | 查询交易历史 |
| `/wm economy [process]` | 查看或处理经济系统状态 |
| `/wm resetpassword <邮箱>` | 管理员重置网页密码 |

---

## 权限节点

| 节点 | 用途 |
|---|---|
| `webmarket.use` | 基础命令权限 |
| `webmarket.resetpassword` | 重置网页密码 |
| `webmarket.economy.view` | 查看经济系统状态 |
| `webmarket.economy.process` | 处理离线经济记录 |
| `webmarket.restrict` | 管理市场限制 |
| `webmarket.marketlogs` | 查询玩家/材质交易日志 |
| `webmarket.marketlogs.self` | 查询自己的交易日志 |
| `webmarket.iconcache` | 管理网页图标缓存 |
| `webmarket.blockitem` | 管理禁止上架物品 |
| `webmarket.money.balance` | 查看自己的余额 |
| `webmarket.money.others` | 查看其他玩家余额 |
| `webmarket.money.pay` | 金币转账 |
| `webmarket.money.top` | 查看财富排行榜 |
| `webmarket.money.history` | 查看自己的交易记录 |
| `webmarket.money.history.others` | 查看其他玩家交易记录 |
| `webmarket.money.admin` | 管理员经济命令 |

---

## bStats

![bStats](https://bstats.org/signatures/bukkit/webmarket.svg)

---