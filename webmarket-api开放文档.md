# WebMarket 附属插件快速开发

## 1. 依赖

```xml
<dependency>
    <groupId>cn.kurt6</groupId>
    <artifactId>webmarket-api</artifactId>
    <version>2.4.2</version>
    <scope>provided</scope>
</dependency>
```

## 2. 主类最小示例

```java
public class MyAddonPlugin extends JavaPlugin implements WebMarketAddon {

    private static final String KEY = "my_addon";

    private static final AddonDescriptor DESCRIPTOR = new AddonDescriptor(
            KEY,
            "my-addon",
            List.of(),
            "addons.entries.my_addon.title",
            "addons.entries.my_addon.description",
            List.of("/addon-assets/" + KEY + "/js/my-addon.js"),
            List.of("/addon-assets/" + KEY + "/css/my-addon.css"),
            50
    );

    @Override
    public void onEnable() {
        Bukkit.getServicesManager().register(WebMarketAddon.class, this, this, ServicePriority.Normal);
    }

    @Override
    public void onDisable() {
        Bukkit.getServicesManager().unregister(WebMarketAddon.class, this);
    }

    @Override public Plugin getPlugin() { return this; }
    @Override public AddonDescriptor describe() { return DESCRIPTOR; }

    @Override
    public Map<String, Object> resolveIntegrationState(Integer webUserId) {
        return Map.of("enabled", true);
    }
}
```

## 3. 目录

- 入口 SPI：`cn.kurt6.webmarket.api.addon`
- 背包 bridge：`cn.kurt6.webmarket.api.addon.inventory`
- 用户 bridge：`cn.kurt6.webmarket.api.addon.user`
- 平台 bridge：`cn.kurt6.webmarket.api.addon.platform`
- 经济 bridge：`cn.kurt6.webmarket.api.addon.economy`
- 待领取 bridge：`cn.kurt6.webmarket.api.addon.pending`

## 4. 如果要用宿主背包能力

```java
RegisteredServiceProvider<InventorySnapshotBridge> registration =
        Bukkit.getServicesManager().getRegistration(InventorySnapshotBridge.class);
InventorySnapshotBridge bridge =
        registration == null ? null : registration.getProvider();
```

可用 bridge：

- `InventorySnapshotBridge`
- `InventoryMutationBridge`
- `WebMarketUserBridge`
- `PlatformBridge`
- `EconomyBridge`
- `PendingItemBridge`

## 5. 什么时候用

- 做附属入口：实现 `WebMarketAddon`
- 读玩家背包：`InventorySnapshotBridge`
- 管理员删玩家物品：`InventoryMutationBridge`
- 查用户资料/在线状态：`WebMarketUserBridge`
- 查跨服状态：`PlatformBridge`
- 查余额：`EconomyBridge`
- 查待领取/触发领取：`PendingItemBridge`

## 6. 打包

```bash
mvn -DskipTests package
```

把生成的 jar 放进 `plugins/` 即可。
