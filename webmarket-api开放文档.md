# WebMarket API 开放文档

本文档面向独立附属插件作者，说明当前 `webmarket-api` 对外暴露的 SPI、宿主侧路由契约，以及推荐的 `pom.xml` 接入方式。

本文档按当前仓库中的真实源码整理，接口源以 `cn.kurt6.webmarket.api.addon.WebMarketAddon` 与 `cn.kurt6.webmarket.api.addon.AddonDescriptor` 为准。

## 1. 接入方式

```xml
<dependency>
    <groupId>cn.kurt6</groupId>
    <artifactId>webmarket-api</artifactId>
    <version>2.4.0</version>
    <scope>provided</scope>
</dependency>
```

## 2. 最小骨架

### `plugin.yml`

```yaml
name: MyAddon
main: cn.example.myaddon.MyAddonPlugin
version: 1.0.0
api-version: 1.20
depend: [WebMarket]
```

### 主类

```java
package cn.example.myaddon;

import cn.kurt6.webmarket.api.addon.AddonDescriptor;
import cn.kurt6.webmarket.api.addon.WebMarketAddon;
import org.bukkit.Bukkit;
import org.bukkit.plugin.Plugin;
import org.bukkit.plugin.ServicePriority;
import org.bukkit.plugin.java.JavaPlugin;

import java.io.IOException;
import java.io.InputStream;
import java.nio.charset.StandardCharsets;
import java.util.List;
import java.util.Map;
import java.util.Set;

public final class MyAddonPlugin extends JavaPlugin implements WebMarketAddon {

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
        Bukkit.getServicesManager().register(
                WebMarketAddon.class,
                this,
                this,
                ServicePriority.Normal
        );
    }

    @Override
    public void onDisable() {
        Bukkit.getServicesManager().unregister(WebMarketAddon.class, this);
    }

    @Override
    public Plugin getPlugin() {
        return this;
    }

    @Override
    public AddonDescriptor describe() {
        return DESCRIPTOR;
    }

    @Override
    public Map<String, Object> resolveIntegrationState(Integer webUserId) {
        return Map.of("enabled", true);
    }

    @Override
    public Set<String> getPublicReadonlyPaths() {
        return Set.of("", "/history");
    }

    @Override
    public Map<String, Object> handleApiRequest(String method,
                                                String path,
                                                Map<String, Object> body,
                                                Integer webUserId) {
        return Map.of(
                "status", 200,
                "success", true,
                "message", "Hello from " + KEY
        );
    }

    @Override
    public byte[] getWebAsset(String relativePath) {
        try (InputStream in = getResource("web/" + relativePath)) {
            return in == null ? null : in.readAllBytes();
        } catch (IOException exception) {
            return null;
        }
    }

    @Override
    public Map<String, String> getPageHtmlFragments() {
        try (InputStream in = getResource("web/page-fragments/my-addon.html")) {
            if (in == null) {
                return Map.of();
            }
            return Map.of("my-addon", new String(in.readAllBytes(), StandardCharsets.UTF_8));
        } catch (IOException exception) {
            return Map.of();
        }
    }

    @Override
    public Map<String, Map<String, String>> getWebLangBundles() {
        return Map.of(
                "zh_cn", Map.of(
                        "addons.entries.my_addon.title", "我的附属",
                        "addons.entries.my_addon.description", "示例附属",
                        "my_addon.greeting", "你好"
                ),
                "en_us", Map.of(
                        "addons.entries.my_addon.title", "My Addon",
                        "addons.entries.my_addon.description", "Sample addon",
                        "my_addon.greeting", "Hello"
                )
        );
    }
}
```

## 3. 当前公开接口

### `WebMarketAddon`

```java
public interface WebMarketAddon {
    Plugin getPlugin();
    AddonDescriptor describe();
    Map<String, Object> resolveIntegrationState(Integer webUserId);

    default Map<String, Object> handleApiRequest(String method,
                                                 String path,
                                                 Map<String, Object> body,
                                                 Integer webUserId) { ... }

    default byte[] getWebAsset(String relativePath) { ... }
    default Map<String, String> getPageHtmlFragments() { ... }
    default Map<String, Map<String, String>> getWebLangBundles() { ... }
    default Set<String> getPublicReadonlyPaths() { ... }
}
```

#### `Plugin getPlugin()`

- 返回当前附属插件自己的 Bukkit `Plugin` 实例。
- 宿主会用它过滤已经被禁用的注册项。
- 通常直接 `return this;` 即可。

#### `AddonDescriptor describe()`

- 返回稳定、轻量、最好可缓存的附属描述对象。
- 宿主会在附属枚举、页面路由、资源加载、`/api/config` 组装时频繁读取。
- 不要在这里做数据库查询、IO 或动态大对象构建，推荐 `static final`。

#### `Map<String, Object> resolveIntegrationState(Integer webUserId)`

- 宿主在构造 `/api/config` 的 `addons` 字段时调用。
- `webUserId` 可能为 `null`，表示当前配置请求是匿名访问。
- 返回值里至少要包含 `enabled` 布尔值。
- 其他字段会原样挂到 `config.addons.{key}` 下，供前端读取。

示例：

```java
@Override
public Map<String, Object> resolveIntegrationState(Integer webUserId) {
    boolean enabled = bridgeReady && featureSwitchOn;
    return Map.of(
            "enabled", enabled,
            "authenticated", webUserId != null,
            "has_data", enabled && webUserId != null
    );
}
```

#### `Map<String, Object> handleApiRequest(String method, String path, Map<String, Object> body, Integer webUserId)`

- 处理 `/api/addon/{key}` 与 `/api/addon/{key}/...` 下的附属 API。
- `method` 当前按宿主实现主要会收到 `GET` / `POST`。
- `path` 是完整请求路径，例如 `/api/addon/title_shop/equip`。
- `body` 是已经解析好的 JSON；GET 为 `null`，空 POST 也可能是 `null`。
- `webUserId` 是认证通过后的 Web 用户 id；匿名公开 GET 时可能为 `null`。

返回约定：

- 你可以在返回 map 里放 `status` 指定 HTTP 状态码。
- 如果不写 `status`，宿主默认按 `200` 返回。
- 如果不写 `success`，宿主会按 `status < 400` 自动补一个布尔值。
- 常见字段是 `success`、`message_key`、`message`、`data`。

示例：

```java
@Override
public Map<String, Object> handleApiRequest(String method,
                                            String path,
                                            Map<String, Object> body,
                                            Integer webUserId) {
    if ("GET".equalsIgnoreCase(method) && "/api/addon/my_addon".equals(path)) {
        return Map.of(
                "status", 200,
                "success", true,
                "data", Map.of("server_time", System.currentTimeMillis())
        );
    }
    if ("POST".equalsIgnoreCase(method) && "/api/addon/my_addon/ping".equals(path)) {
        return Map.of("success", true, "message_key", "my_addon.ping_ok");
    }
    return Map.of(
            "status", 405,
            "success", false,
            "message_key", "api.common.method_not_allowed"
    );
}
```

注意：

- 宿主认证在中间件里先做一遍，附属代理里还会用 `Authorization: Bearer <apiKey>` 再校验一遍，避免退出登录后靠旧状态继续操作。
- `/admin/` 子路径除了登录态，还要求这次请求真的带着有效 Bearer API Key。
- 不要把旧的前端缓存或本地状态当成权限依据，最终以服务端当前认证结果为准。

#### `byte[] getWebAsset(String relativePath)`

- 处理 `/addon-assets/{key}/...` 资源请求。
- 传入的是去掉前缀后的相对路径，不带前导 `/`。
- 常见值例如 `js/title-shop.js`、`css/title-shop.css`、`img/icon.png`。
- 返回 `null` 会被宿主当成 `404`。

常见实现：

```java
@Override
public byte[] getWebAsset(String relativePath) {
    try (InputStream in = getResource("web/" + relativePath)) {
        return in == null ? null : in.readAllBytes();
    } catch (IOException exception) {
        return null;
    }
}
```

#### `Map<String, String> getPageHtmlFragments()`

- 处理 `/addon-pages/{key}.html?page={pageId}`。
- key 是 `pageId`，value 是对应页面容器的 `innerHTML`。
- 如果 URL 里不传 `page`，宿主默认取 `describe().pageId()`。
- 这里返回的是页面内部片段，不需要自己再包最外层 `<div id="...-page">`。

单页示例：

```java
@Override
public Map<String, String> getPageHtmlFragments() {
    return Map.of("my-addon", loadUtf8("web/page-fragments/my-addon.html"));
}
```

多页示例：

```java
@Override
public Map<String, String> getPageHtmlFragments() {
    return Map.of(
            "my-addon", loadUtf8("web/page-fragments/my-addon.html"),
            "my-addon-detail", loadUtf8("web/page-fragments/my-addon-detail.html")
    );
}
```

#### `Map<String, Map<String, String>> getWebLangBundles()`

- 外层 key 是语言代码，例如 `zh_cn`、`en_us`。
- 内层 map 是点号分隔的扁平 key。
- 宿主只会把这些 key 深合并进 `/lang/{lang}.json` 根节点，不会自动替你补任何前缀。

这点很重要：

- `addons.entries.my_addon.title` 会被前端以 `translate("addons.entries.my_addon.title")` 取到。
- `my_addon.greeting` 会被前端以 `translate("my_addon.greeting")` 取到。
- 你自己决定命名空间，但要保持稳定，避免和主插件或其他附属冲突。

示例：

```java
@Override
public Map<String, Map<String, String>> getWebLangBundles() {
    return Map.of(
            "zh_cn", Map.of(
                    "addons.entries.my_addon.title", "我的附属",
                    "addons.entries.my_addon.description", "示例附属",
                    "my_addon.greeting", "你好"
            ),
            "en_us", Map.of(
                    "addons.entries.my_addon.title", "My Addon",
                    "addons.entries.my_addon.description", "Sample addon",
                    "my_addon.greeting", "Hello"
            )
    );
}
```

如果你更习惯维护嵌套 JSON，也可以在自己插件内先读 `web/lang/zh_cn.json`、`web/lang/en_us.json`，再像仓库现有附属插件那样展平成扁平 map 返回。

#### `Set<String> getPublicReadonlyPaths()`

- 用来声明哪些附属 API 路径允许匿名 `GET`。
- 这里填写的是 `/api/addon/{key}` 之后的相对路径。
- 根路径写空字符串 `""`。
- 子路径要带前导 `/`，例如 `"/history"`。
- 只对 `GET` 生效，任何写操作仍然要求认证。

示例：

```java
@Override
public Set<String> getPublicReadonlyPaths() {
    return Set.of("", "/history", "/leaderboard");
}
```

实际对应：

- `""` -> `GET /api/addon/my_addon`
- `"/history"` -> `GET /api/addon/my_addon/history`
- `"/leaderboard"` -> `GET /api/addon/my_addon/leaderboard`

## 4. `AddonDescriptor` 字段说明

```java
public record AddonDescriptor(
        String key,
        String pageId,
        List<String> extraPageIds,
        String titleKey,
        String descriptionKey,
        List<String> scriptUrls,
        List<String> styleUrls,
        int order
) { ... }
```

### `key`

- 全局唯一短标识，例如 `title_shop`、`ai_stock`。
- 宿主用它拼出：
  - `/api/addon/{key}/...`
  - `/addon-assets/{key}/...`
  - `/addon-pages/{key}.html`
- 一旦发布后尽量不要再改。

### `pageId`

- 附属主页面 id，例如 `title-shop`。
- 宿主会创建 `<div id="{pageId}-page" class="page">` 容器。
- 你的 `registerAddonPageHandler(pageId, ...)` 和 `getPageHtmlFragments().get(pageId)` 都要对齐这个值。

### `extraPageIds`

- 同一个附属拥有的额外页面 id 列表。
- 适合详情页、新闻页、分区页等多页面场景。
- 宿主会和主页面一起预留容器并按需拉取 HTML 片段。

### `titleKey` / `descriptionKey`

- 用于附加中心卡片标题和描述的翻译 key。
- 宿主会优先使用这里的 key 调 `translate(...)`。
- 如果你想跟当前默认附加中心 fallback 约定保持一致，建议写成：
  - `addons.entries.{key}.title`
  - `addons.entries.{key}.description`

### `scriptUrls` / `styleUrls`

- 需要由宿主前端动态注入的脚本和样式 URL。
- 推荐使用附属自己的资源代理路径：
  - `/addon-assets/{key}/js/...`
  - `/addon-assets/{key}/css/...`
- 会按列表顺序注入。

### `order`

- 附加中心展示排序，数字越小越靠前。
- 当前仓库里的现有附属示例：
  - AI 股市：`10`
  - 称号商店：`20`

### 便利构造器

`AddonDescriptor` 还提供了一个单页简化构造器：

```java
public AddonDescriptor(String key,
                       String pageId,
                       String titleKey,
                       String descriptionKey,
                       List<String> scriptUrls,
                       List<String> styleUrls)
```

它会自动使用：

- `extraPageIds = List.of()`
- `order = 100`

## 5. 宿主路由与返回契约

### API

| 路径 | 宿主侧处理 | 最终进入 |
|---|---|---|
| `/api/addon/{key}` | `AddonProxyHandler` | `handleApiRequest("GET/POST", fullPath, body, webUserId)` |
| `/api/addon/{key}/...` | `AddonProxyHandler` | 同上 |
| `/addon-assets/{key}/...` | `AddonAssetHandler` | `getWebAsset(relativePath)` |
| `/addon-pages/{key}.html?page={pageId}` | `AddonPageFragmentHandler` | `getPageHtmlFragments().get(pageId)` |
| `/lang/{lang}.json` | `LangHandler` | `getWebLangBundles()` 的结果会被深合并 |
| `/api/config` | `AddonManager` | `describe()` + `resolveIntegrationState()` |

### `/api/config` 中的附属输出

宿主会把附属状态整理成：

```json
{
  "addons": {
    "my_addon": {
      "enabled": true,
      "authenticated": true
    },
    "entries": [
      {
        "key": "my_addon",
        "page": "my-addon",
        "extra_pages": [],
        "enabled": true,
        "title_key": "addons.entries.my_addon.title",
        "description_key": "addons.entries.my_addon.description",
        "scripts": ["/addon-assets/my_addon/js/my-addon.js"],
        "styles": ["/addon-assets/my_addon/css/my-addon.css"],
        "order": 50
      }
    ]
  }
}
```

规则：

- `resolveIntegrationState()` 返回的 `enabled` 为 `true`，该附属才会进入 `entries`。
- `entries` 会按 `order` 升序排序。
- 额外字段会保留给前端读取。

## 6. 前端接入规则

宿主前端 `bootstrapAddons()` 会做这些事：

1. 读取 `/api/config` 的 `addons.entries`
2. 预加载 `styleUrls`
3. 为 `pageId` 和 `extraPageIds` 拉取 `/addon-pages/{key}.html?page={pageId}`
4. 把 HTML 片段注入到 `#addon-pages-mount`
5. 动态注入 `scriptUrls`
6. 把页面加入内部路由与初始化状态表

所以你的前端脚本应主动注册页面处理器：

```javascript
(function () {
    'use strict';

    function init() {
        const button = document.getElementById('my-addon-btn');
        if (!button) {
            return false;
        }
        button.addEventListener('click', async () => {
            const response = await fetch('/api/addon/my_addon/history');
            console.log(await response.json());
        });
        return true;
    }

    function refresh() {}
    function cleanup() {}

    if (typeof window.registerAddonPageHandler === 'function') {
        window.registerAddonPageHandler('my-addon', {
            init,
            refresh,
            cleanup
        });
    }
})();
```

约束：

- `registerAddonPageHandler()` 的 `pageId` 必须和 `AddonDescriptor.pageId()` 或 `extraPageIds()` 一致。
- `init()` 返回 `true` 后宿主才会把该页标记为已初始化。
- 切页刷新逻辑走 `refresh()`，离页清理由 `cleanup()` 负责。

## 7. 资源与目录建议

推荐目录：

```text
my-addon/
├── pom.xml
└── src/main/
    ├── java/cn/example/myaddon/MyAddonPlugin.java
    └── resources/
        ├── plugin.yml
        └── web/
            ├── css/
            │   └── my-addon.css
            ├── js/
            │   └── my-addon.js
            ├── lang/
            │   ├── en_us.json
            │   └── zh_cn.json
            └── page-fragments/
                └── my-addon.html
```

HTML 片段只写页面内部内容，例如：

```html
<h2 data-i18n="addons.entries.my_addon.title">我的附属</h2>
<p data-i18n="my_addon.greeting">你好</p>
<button id="my-addon-btn" type="button">Click</button>
```

## 8. 生命周期与线程模型

按当前宿主实现，这些方法都运行在 Web HTTP 工作线程，不是 Bukkit 主线程：

- `describe()`
- `resolveIntegrationState(...)`
- `handleApiRequest(...)`
- `getWebAsset(...)`
- `getPageHtmlFragments()`
- `getWebLangBundles()`

建议：

- 不要在这些方法里直接做阻塞式主线程操作。
- 需要和 Bukkit 主线程交互时，自己调度回主线程。
- 高频读取的描述对象、HTML 片段、静态资源字节、语言 map 最好缓存。
- 返回值尽量用不可变集合，避免被错误共享修改。

## 9. 开发边界

推荐做法：

- 只依赖 `webmarket-api` 公开的 SPI。
- 通过稳定 URL、稳定页面 id、稳定 i18n key 与主插件协作。
- 必要时只反射主插件明确暴露的稳定桥接方法。

不推荐做法：

- 直接依赖主插件内部模型、DAO、Service 实现类。
- 假设主插件内部包名、字段名、混淆前类名永远不变。
- 把附属状态安全性建立在前端缓存、本地存储或旧页面残留数据上。

## 10. 建议配套阅读

- `addons/附属插件快速开发指南.md`
- `addons/附属插件开发说明.md`

如果你主要关心“先做出一个最小可跑附属”，先看快速开发指南；如果你关心“每个 SPI 方法到底怎么被宿主调用”，以本文档为主。
