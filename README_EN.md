# WebMarket

[Demo video](https://www.youtube.com/watch?v=tvTJZuOYvno) /
[Demo site](https://sd.kurt6.cn)

## Free / Paid Version Comparison

[Purchase link](https://www.patreon.com/posts/154367931) /
[afdian link](https://afdian.com/item/ab436e0484a511f0882b52540025c377)

| Feature                         | Free Version | Paid Version |
|---------------------------------|--------------|--------------|
| Basic Global Market (Player Market, limited to 100 items) | Supported     | Supported    |
| Offline Operation               | Supported     | Supported    |
| In-game GUI                     | Not Supported | Supported    |
| Buy Request System              | Not Supported | Supported    |
| Auction House                   | Not Supported | Supported    |
| Official Shop Sell / Buy Back   | Not Supported | Supported    |
| Buff Shop                       | Not Supported | Supported    |
| Special Items / Perks Area      | Not Supported | Supported    |
| Cross-server Functionality      | Not Supported | Supported    |
| Player Personalization (Permission Group Support) | Not Supported | Supported    |
| Points Trading                  | Not Supported | Supported    |

---

Feature-rich Minecraft web market plugin, offering a basic free version and a full-featured paid version. The web interface is compatible with mobile display.

Supports 1.20+ Paper / Folia / Spigot / Bukkit / Purpur servers.

The free version focuses on the basic web market, inventory viewing, claiming, transaction logs, accounts, and economy capabilities. Players can list a maximum of 100 items simultaneously in the player market, and points trading is not supported. The paid version additionally offers GUI, buy requests, auctions, official shop, Buff shop, special items area, and cross-server capabilities.

The web interface supports displaying custom item icons for some ItemsAdder, CraftEngine, vanilla, and mod items; in-game GUI is a paid version feature.

Supports PlayerPoints and Vault currency trading. The free version only supports currency trading; points trading is exclusive to the paid version. The paid version's basic market, buy requests, auctions, official shop, Buff shop, and special items shop all support independent pricing and settlement.

Supports usage in hybrid modpacks (mod item icon resources and localization may not be fully retrieved, requiring manual addition in the web directory; an included EXE tool can automatically complete some resource additions).

---

## Key Features

- **Offline Support**

  When players are offline, inventory/ender chest data is stored in real-time, allowing the web interface to view and perform basic market operations.

- **Full NBT**

  Durability info, enchantments, enchantment book effects, potion effects, custom names, detailed information of items inside containers (shulker boxes, bundles) are all preserved and displayed on the web page. Supports prioritizing custom-named image resources, falling back to displaying the item's material image if not found (automatically excludes player-named items).

- **Container Listing**

  One-click listing of entire boxes/bundles, with real-time preview of items inside the container on the web page; the paid version's in-game GUI also supports container preview.

- **Official Shop Dynamic Pricing (Paid Version)**

  Calculation formula: Dynamic Price = Base Price × (1 + sigmoid(3-day trend) × Sensitivity × Trend Weight)

- **Buff Shop + Special Items/Perks Area (Paid Version)**

  The Buff shop allows purchasing buffs per second, requiring the player to be online.

  In the Special Items/Perks area, upon purchase, one or more custom commands are executed, supporting the {player} variable, convenient for purchasing perks.

  After creating a special item, accounts with admin privileges can directly modify all information on the web page.

- **Buy Request (Paid Version)**

  Can be created in two ways:

  ① Via the command `/sg <quantity> <unit price>` while holding the item.
  ② Directly create the buy request on the web page.

---

## 🛒 Module Description

| Module               | Version                 | Description                                                                                                                               |
|----------------------|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| Player Trading Market| Free / Paid             | Players freely list/buy others' items, supports custom transaction taxes, whitelist/blacklist modes.                                      |
| Buy Request          | Paid                    | Players can post buy requests to be fulfilled by other players.                                                                          |
| Auction House        | Paid                    | Auction area, supports custom transaction taxes, whitelist/blacklist modes.                                                               |
| Official Shop        | Paid                    | Official Sell Area & Official Buyback Area & Buff Area & Special Items Area, official sell/buyback areas can enable dynamic pricing system. |

---

## 🎒 Inventory Management

- Real-time web viewing of online/offline player inventory/ender chest.
- Displays durability, enchantments, Lore, items inside containers.
- One-click selling of inventory/ender chest items directly to the market; paid version also supports related auction flows.

---

## 🏆 Leaderboards

| Leaderboard     | Description                         |
|-----------------|-------------------------------------|
| Wealth Leaderboard | Server's richest players.           |
| Trade Leaderboard  | Players with the highest transaction volume. |
| Sell Leaderboard   | Players who have sold the most.       |
| Buy Leaderboard    | Players who have bought the most.     |

---

## 🔐 Account System

- Supports AuthMe, login via game name or email. Account automatically binds upon login and cannot be unbound.
- In-game command `/wm register <email> <password> [username]` registers a web account, automatically binding it (unbindable). Username is optional, defaults to game name.
- Web page email registration requires manual binding to a game account, can be unbound.
- API key for authentication-free login.

---

## Command List

All commands start with `/wm`. You can also omit `/wm` and use shorthand commands.

| Command <required> [optional] | Description |
|---|---|
| `/wm`, `/wm gui`, `/market` | Opens the in-game shop GUI. Can be disabled via permission node `webmarket.gui`. |
| `/wm help` | View help for commands available to your permissions. |
| `/wm bind <verification_code>` | Bind web account to game account. |
| `/wm register <email> <password> [username]` | Register web account in-game, automatically binds (unbindable). Username optional, defaults to game name. |
| `/wm claim` | Claim items purchased from the web (used by offline players or online players with full inventory). |
| `/wm sj <quantity> <unit price> [currency/points]` | Quickly list the item in hand (player use, batch listing possible). |
| `/wm sg <quantity> <unit price> [currency/points]` | Quickly create a buy request for the item in hand (player use). |
| `/wm pm <quantity> <starting bid> <time(1-48 hours)> [buyout price] [currency/points]` | Quickly auction the item in hand (player use, batch auction possible). |
| `/wm sell <unit price> [personal limit] [total stock] [personal limit reset period h] [currency/points] [cross-server/this-server]` | OP only: Add the item in hand to the Official Shop sell area (full NBT recorded, recommend holding 1 item). Default this-server only; add `cross-server` to allow purchase from other servers. Personal limit: leave empty or -1 for unlimited. Total stock: leave empty or -1 for unlimited. Reset period: hours, 0 or empty for no reset. |
| `/wm recycle <unit price> [personal limit] [total buyback] [personal limit reset period h] [currency/points] [cross-server/this-server]` | OP only: Add the item in hand to the Official Shop buyback area (full NBT recorded, recommend holding 1 item). Default this-server only; add `cross-server` to allow buyback from other servers. Personal limit: leave empty or -1 for unlimited. Total buyback: leave empty or -1 for unlimited. Reset period: hours, 0 or empty for no reset. |
| `/wm buff <buff type> <level> <price per second> [minimum seconds] [maximum seconds] [personal limit seconds] [total stock seconds] [reset period h] [currency/points] [cross-server/this-server]` | OP only: Add item to Official Shop Buff area. Default this-server only; add `cross-server` to allow purchase from other servers. Type `/buff` in-game for detailed help. |
| `/wm specialitem <name> <description> <price> <icon material> <command1 command2 ...> [personal limit] [total stock] [reset period h] [currency/points] [cross-server/this-server]` | OP only: Add item to Official Shop Special Items area. Default this-server only; add `cross-server` to allow purchase from other servers. Supports {player} variable, separate multiple commands with `\|`. Type `/specialitem` in-game for detailed help. |
| `/wm root <email>` | OP only: Grant admin privileges to specified email user (can remove any player's items, delete official shop items). |
| `/wm unroot <email>` | OP only: Remove admin privileges from specified email user. |
| `/wm resetpassword <email>` | OP only: Reset password for specified email user. User can change password on web page later. |
| `/wm marketlogs me` | Query own transaction logs. Filters: `-type:` (buy, sell, list, delist, auction, request, buff, special, shop, all), `-time:` (today, yesterday, week, month, custom:yyyy-MM-dd, custom:yyyy-MM-dd:yyyy-MM-dd). |
| `/wm marketlogs <player name> [page] [filters]` | OP only: Query specified player's transaction logs. Filters same as above. Type `/marketlogs` in-game for GUI. |
| `/wm marketlogs-material <item material> [page] [filters]` | OP only: Query transaction logs for specified item material. Filters: `-type:` (market, auction, buy_request, official_buy, official_sell, all), `-time:` (today, yesterday, week, month, custom:yyyy-MM-dd, custom:yyyy-MM-dd:yyyy-MM-dd). Type `/marketlogs-material` in-game for GUI. |
| `/wm restrict` | OP only: Restrict specific players from creating market listings, buy requests, or auctions. Type `/restrict` in-game for detailed help. |
| `/wm blockitem` | OP only: Block the item in hand from being listed, used in buy requests, or auctions, preventing certain menu items from being listed. Type `/blockitem` in-game for detailed help. |
| `/wm iconcache` | OP only: Manage WebMarket's automatically generated web icon cache, including viewing status, clearing cache, and cleaning expired cache. |

| Built-in Economy Commands `/wm money` (also `/wm bal`) | Description |
|---|---|
|`/wm money help` | View WebMarket economy system help. |
|`/wm money` | View balance. |
|`/wm money <player>` | View another player's balance. |
|`/wm money pay <player> <amount> [reason]` | Transfer funds. |
|`/wm money top [page]` | Wealth leaderboard. |
|`/wm money history [player] [page]` | Transaction history. |
|`/wm money set <player> <amount> [reason]` | OP only: Set balance. |
|`/wm money give <player> <amount> [reason]` | OP only: Give money. |
|`/wm money take <player> <amount> [reason]` | OP only: Take money. |

---

## Permission Nodes

| Node | Purpose |
|---|---|
| `webmarket.sell` | Use `/sell` |
| `webmarket.recycle` | Use `/recycle` |
| `webmarket.root` | Use `/root` and `/unroot` |
| `webmarket.resetpassword` | Use `/resetpassword` |
| `webmarket.marketlogs` | Use `/marketlogs` and `/marketlogs-material` |
| `webmarket.marketlogs.self` | Query own transaction logs (`/marketlogs me` or GUI without args) |
| `webmarket.restrict` | Use `/restrict` |
| `webmarket.buff` | Use `/buff` |
| `webmarket.specialitem` | Use `/specialitem` |
| `webmarket.blockitem` | Use `/blockitem` |
| `webmarket.iconcache` | Use `/iconcache` |
| `webmarket.gui` | Use `/wm gui` |
| `webmarket.use` | Basic command permissions. |
| `webmarket.publish.points` | Allow listing points items/points buy requests/points auctions. Open by default without LuckPerms; managed by permissions plugin if installed. |
| `webmarket.money.balance` | View own balance. |
| `webmarket.money.others` | View other players' balances. |
| `webmarket.money.pay` | Transfer to other players. |
| `webmarket.money.top` | View wealth leaderboard. |
| `webmarket.money.history` | View own transaction history. |
| `webmarket.money.history.others` | View other players' transaction history. |
| `webmarket.money.admin` | Admin economy commands (set/give/take). |

---

## PlaceholderAPI Placeholders

After installing `PlaceholderAPI`, the plugin automatically registers `%webmarket_*%` placeholders.

Currently supported wealth/balance-related placeholders:

| Placeholder | Description |
|---|---|
| `%webmarket_balance%` | Current player's currency balance, raw number format. |
| `%webmarket_balance_formatted%` | Current player's currency balance, formatted using the economy system. |
| `%webmarket_rank%` | Player's rank on the wealth leaderboard, returns `0` if not on the board. |
| `%webmarket_top_1_name%` | Name of the #1 player on the wealth leaderboard. |
| `%webmarket_top_1_player%` | Same as `%webmarket_top_1_name%`. |
| `%webmarket_top_1_balance%` | Balance of the #1 player on the wealth leaderboard, raw number format. |
| `%webmarket_top_1_balance_formatted%` | Balance of the #1 player on the wealth leaderboard, formatted. |
| `%webmarket_top_1_rank%` | Returns the rank number itself, e.g., `1` for 1st place. |

Note:
- Replace `1` with any rank number, e.g., `%webmarket_top_5_name%`, `%webmarket_top_10_balance%`.
- Placeholders are currently based on the currency wealth leaderboard, not including points.
- To avoid frequent database scans during scoreboard refreshes, wealth leaderboard placeholders use caching; cache time is configurable via `placeholderapi.wealth_cache_seconds`, default `60` seconds. Setting to `0` disables caching, each request triggers an async refresh.

---

## Player Personalization (Permission Group Support, Paid Version)

Set listing limits, tax rates, validity days, etc., for players via permission groups:

### Sell System

- `webmarket.limit.market.sell.max_listings.<number>`
  Max listing count.
- `webmarket.limit.market.sell.max_duration_days.<days>`
  Max duration in days.
- `webmarket.tax.market.sell.money.<rate>`
  Currency sell tax rate.
- `webmarket.tax.market.sell.points.<rate>`
  Points sell tax rate.

### Buy Request System

- `webmarket.limit.market.buy.max_requests.<number>`
  Max buy request count.
- `webmarket.limit.market.buy.max_duration_days.<days>`
  Max duration in days.
- `webmarket.tax.market.buy.money.<rate>`
  Currency buy request tax rate.
- `webmarket.tax.market.buy.points.<rate>`
  Points buy request tax rate.

### Auction House

- `webmarket.limit.auction.max_listings.<number>`
  Max auction count.
- `webmarket.limit.auction.max_duration_hours.<hours>`
  Max auction duration in hours.
- `webmarket.tax.auction.money.<rate>`
  Currency auction tax rate.
- `webmarket.tax.auction.points.<rate>`
  Points auction tax rate.

---

## Cross-server Configuration

In `config.yml`, use `cross_server` to control cross-server behavior:

- Cross-server functionality only supports **MySQL**. If `database.type` is not `MySQL`, cross-server is automatically disabled at runtime even if `cross_server.enabled: true`.
- `cross_server.mode`: `isolated` = market/auction data isolated per server; `shared` = market/auction data shared across servers, purchased items go to a claiming area.
- `cross_server.server_name`: Unique identifier for the current server.
- `cross_server.server_aliases`: List of old names for the current server. After changing `server_name`, add old names here for compatibility with old offline inventory keys and old `server_name` data.
- `cross_server.master_server_name`: In `shared` mode, the name of the master server; market/auction configurations are synced from the master server.
- `cross_server.item_sync_enabled`: Whether to enable external cross-server item sync. When disabled, the plugin manages its own server-isolated offline inventory; when enabled, the plugin stops relying on its own offline inventory snapshots and disables some player offline item operations to avoid conflicts with external sync solutions.
- `cross_server.known_servers`: List of known servers for server selection dropdowns in the web UI and GUI.
- After enabling cross-server, certain global tasks like dynamic price resets/daily refreshes are only executed by the server designated as `master_server_name` to avoid duplicate updates across multiple servers.

---

## Purchase and Activation

1. Purchase on Afdian.
2. Send your Afdian order number to QQ `1758426625` or email `1758426625@qq.com` to receive an activation code.
3. Fill in the activation code in the `activation_code` field in `config.yml` to use the plugin.

---

## Purchase Notes

1. Plugin usage requires an activation code. Each activation code is limited to one IP address at a time.
2. If activation fails after changing IP, please wait at least 40 minutes before trying again.
3. If your activation code is abused, the developer has the right to disable it.

---

## bStats

![bStats](https://bstats.org/signatures/bukkit/webmarket.svg)

---

## Configuration File

```yaml
activation_code: "" # Activation code

# Plugin language configuration
# Options: zh_cn, en_us
language: "zh_cn"

# Database configuration
database:
  type: "SQLite" # SQLite or MySQL
  # MySQL configuration (use for high player counts, requires 8.0+)
  host: "localhost"
  port: 3306
  database: "webmarket"
  username: "root"
  password: ""
  # Connection pool settings
  pool:
    max_size: 10
    min_idle: 2
    connection_timeout: 30000
    idle_timeout: 600000
    max_lifetime: 1800000
    leak_detection_threshold: 60000

# API server configuration
api:
  enabled: true # Whether to enable HTTP API / Web service
  enable_on_secondary_shared_server: false # Whether secondary servers in shared mode also start HTTP service; usually only master needs it
  port: 8880 # Server listening port
  host: "0.0.0.0" # Server binding address, "0.0.0.0" listens on all interfaces
  worker_threads: 4 # Number of threads for API request processing
  queue_capacity: 1600 # Request queue capacity
  ssl:
    enabled: false # Whether to enable HTTPS. If false, uses plain HTTP.
    key_store_path: "ssl/keystore.p12" # Keystore path. Absolute path or path relative to plugins/WebMarket/
    key_store_password: "" # Keystore password
    key_password: "" # Private key password. If empty, defaults to key_store_password
    key_store_type: "PKCS12" # Keystore type, e.g., PKCS12 / JKS
    protocol: "TLS" # SSLContext protocol, generally keep as TLS

# Player identity (binding) matching mode
player_identity:
  mode: "name" # uuid = identify by UUID (recommended for online-mode servers), name = identify by game name (recommended for offline-mode servers)

# Web frontend configuration
# To customize logo icon, place image in plugins/WebMarket/web-assets/logo/logo.png
web:
  # Website logo text
  logo_text: 'WebMarket'
  # Whether to prioritize using custom name image resources. Place in plugins/WebMarket/web-assets/custom-images/<custom_name>.png (without color codes)
  # When enabled, prioritizes images for custom-named items, falling back to item material image if not found (excluding player-named items)
  use_custom_name_image: true
  # Whether to allow custom names to override material names. When enabled, displays custom name primarily, no longer showing "Custom Name" line (excluding player-named items)
  use_custom_name_override: true
  # Whether to enable backend generation and caching of web item icons. Results saved to plugins/WebMarket/web-assets/generated-icons/
  generated_item_icons:
    enabled: true
    # Note: Enabling this may leak icon resources from CraftEngine/ItemsAdder etc.
    # Whether to allow generating web icons for ItemsAdder custom items
    itemsadder_enabled: false
    # Whether to allow generating web icons for CraftEngine custom items
    craftengine_enabled: false
    # Whether to allow extracting web icons from server vanilla resources
    vanilla_enabled: true
    # Whether to attempt downloading from official Minecraft client resources and cache them if local vanilla resources are missing
    vanilla_download_enabled: true
    # Vanilla client download source list. Tried in order, official source used as final fallback.
    # Provide base address for each source; the program automatically appends Mojang/Piston paths.
    vanilla_download_sources:
      - "https://bmclapi2.bangbang93.com"
      - "https://launchermeta.mojang.com"
    # Whether to allow extracting web icons and model overrides from world datapacks
    datapack_enabled: true
    # Whether to allow extracting web icons from hybrid modpack mods resources
    hybrid_mod_enabled: true
    # Whether to output debug logs for CE/IA/resource hits
    debug_logging: false
    # Whether to enable automatic cleanup of icon cache files
    cleanup_enabled: true
    # Maximum age in days for files in generated-icons directory, 0 disables automatic cleanup for this directory
    generated_icons_max_age_days: 0
    # Maximum age in days for files in vanilla-cache directory, 0 disables automatic cleanup for this directory
    vanilla_cache_max_age_days: 30

# Cross-server configuration
cross_server:
  enabled: false # Whether to enable cross-server support (MySQL only, automatically disabled with SQLite)
  mode: "isolated" # isolated = isolate by server (only aggregate items), shared = full cross-server sharing
  server_name: "server-1" # Unique name for the current server
  server_aliases: [] # List of old server name aliases. Add old names here after changing server_name for compatibility with old offline inventory and old server_name records
  master_server_name: "server-1" # Master server name
  item_sync_enabled: false # Whether an external cross-server item sync solution is installed. Enabling disables the plugin's built-in offline inventory snapshot mechanism: no longer saves/restores offline inventory and prevents players from performing operations that require direct inventory item removal while offline (e.g., market listing, auction creation, selling to buy requests, official shop buyback)
  economy_sync_enabled: false # Whether economy balance is shared across servers. In isolated mode, when set to false, currency balance and wealth leaderboard are stored and counted independently per server; points read directly from local PlayerPoints, unaffected by this config.
  transaction_sync_enabled: false # Whether transaction statistics are shared across servers. In isolated mode, when set to false, leaderboard trade/sell/buy statistics are isolated per server.
  known_servers: # List of servers selectable in frontend/GUI
    - "server-1"

# Built-in economy system configuration
simple_economy:
  # For cross-server, it's recommended to use the built-in economy first
  # Whether to enable built-in Vault economy system (used when no external economy plugin like CMI, Essentials is present)
  # If you have an external economy plugin but enable this, the plugin will still use the built-in economy for processing.
  # You can also disable CMI's economy and enable this plugin's economy; both are compatible.
  enabled: false
  starting_balance: 100.0  # Initial balance for new players
  max_balance: 999999999.0  # Maximum balance limit
  min_transfer: 0.01  # Minimum transfer amount
  currency_singular: "金币"  # Currency singular name
  currency_plural: "金币"    # Currency plural name
  # Transaction history retention days (-1 for permanent)
  transaction_history_days: 30

# Market settings
market:
  enabled: true # Global player market switch
  broadcast_create_message: true # Whether to send a clickable global notification when a player lists an item
  tax_payer: "seller" # Tax bearer: seller = seller pays (buyer pays listed price), buyer = buyer pays (buyer pays listed price + tax)
  tax_rates:
    money: 0.01 # Currency transaction tax rate
    points: 0.00 # Points transaction tax rate (points settled as integers, non-zero tax rate rounds to integer tax amount)
  max_items_per_page: 24 # Number of items loaded per page
  max_listing_duration: 14 # Maximum listing duration in days
  max_listings_per_player: 10 # Maximum listings per player
  listing_cooldown_seconds: 1 # Listing cooldown in seconds
  # Item listing restrictions
  item_restrictions:
    # Item restriction mode:
    # - "none": No restrictions (default)
    # - "whitelist": Only allow items in the list
    # - "blacklist": Block items in the list
    mode: "none"
    # Restriction list (determined by mode)
    items:
      - "minecraft:bedrock"
      - "minecraft:command_block"
  # Buy request configuration
  buy_request:
    enabled: true # Whether to enable buy request functionality
    broadcast_create_message: true # Whether to send a clickable global notification when a player creates a buy request
    tax_payer: "seller" # Tax bearer: seller = seller pays (seller receives price - tax), buyer = buyer pays (seller receives listed price)
    tax_rates:
      money: 0.02 # Currency buy request transaction tax rate
      points: 0.00 # Points buy request transaction tax rate (points settled as integers, tax rounds)
    max_quantity: 99999 # Maximum quantity for a single buy request
    max_requests_per_player: 3 # Maximum buy requests per player
    max_request_duration: 7 # Maximum buy request duration in days
    request_cooldown_seconds: 1 # Buy request creation cooldown in seconds
    # Buy request item restrictions
    item_restrictions:
      mode: "none" # none, whitelist, blacklist
      items:
        - "minecraft:bedrock"
        - "minecraft:command_block"

# Auction house configuration
auction:
  enabled: true # Global auction house switch
  broadcast_create_message: true # Whether to send a clickable global notification when a player creates an auction
  tax_payer: "seller" # Tax bearer: seller = seller pays (buyer pays listed price), buyer = buyer pays (buyer pays listed price + tax)
  tax_rates:
    money: 0.03 # Currency auction tax rate
    points: 0.00 # Points auction tax rate (points settled as integers, tax rounds)
  max_items_per_page: 24 # Number of items loaded per page
  max_listings_per_player: 10 # Maximum concurrent auctions per player
  listing_cooldown_seconds: 1 # Listing cooldown in seconds
  max_duration_hours: 48 # Maximum auction duration in hours
  # Auction listing restrictions
  item_restrictions:
    mode: "none" # none, whitelist, blacklist
    items:
      - "minecraft:bedrock"
      - "minecraft:command_block"

# Offline inventory configuration
offline_inventory:
  enabled: true  # Whether to enable offline inventory
  ender_chest_display_enabled: true # Whether to display ender chest items at the bottom of the web inventory page
  ender_chest_offline_enabled: true # Whether to enable ender chest offline snapshot display/offline selling & auction

# Official shop configuration
official_shop:
  # Dynamic pricing system configuration
  dynamic_pricing:
    # Whether to enable the dynamic pricing system
    # Uses 3-day weighted average and sigmoid function for smooth changes
    # Dynamic Price = Base Price × (1 + sigmoid(3-day trend) × Sensitivity × Trend Weight)
    enabled: true

    # Price reset strategy
    # false: No reset (price changes continuously based on transaction volume)
    # daily: Reset daily (first check after 00:00 resets to base price)
    # weekly: Reset weekly (resets to base price on Monday)
    # monthly: Reset monthly (resets to base price on the 1st)
    restart: false

    # Transaction activity algorithm configuration
    activity:
      # Sensitivity (0.01-1.0)
      # Higher values mean transaction volume changes have a greater impact on price
      # Recommended value: 0.05-0.2
      sensitivity: 0.1

      # Daily transaction volume threshold
      # Price fluctuations only start when daily volume reaches this value
      # Prevents drastic fluctuations from a few transactions, recommended 1-10
      daily_volume_threshold: 1

    # Global price protection (final price limits)
    price_protection:
      # Whether to enable price floor
      enable_floor: true

      # Minimum price multiplier (relative to base price)
      # Algorithm dynamically adjusts based on price volatility:
      # - High volatility (>30%): limits to 0.7-1.5x base price
      # - Medium volatility (>10%): limits to 0.5-2.0x base price
      # - Low volatility: uses configured multiplier value
      min_price_multiplier: 0.5

      # Whether to enable price ceiling
      enable_ceiling: true

      # Maximum price multiplier (relative to base price)
      # Also dynamically adjusted based on volatility
      max_price_multiplier: 2.0

# Item related configuration
items:
  # Maximum stack size check
  max_stack_size_check: true
  # Minimum allowed quantity per listing
  min_quantity: 1
  # Maximum allowed quantity per listing
  max_quantity: 2304
  # Price limits
  min_price: 0.01
  max_price: 10000000.0

security:
  # API key default validity period (days)
  api_key_expiry_days: 7
  # Password encryption strength (iterations, higher is more secure but more performance intensive)
  encryption_iterations: 10000
  # Whether to enable email whitelist (only whitelisted domains can register)
  email_whitelist_enabled: false
  # Email domain whitelist (domain only, without @)
  # Example: ["qq.com", "gmail.com"]
  email_whitelist_domains:
    - "qq.com"
  # Per-IP registration limit (max accounts per IP, 0 for unlimited)
  registration_limit_per_ip: 2
  # Whether to allow registration via web form (disabling allows only AuthMe registration and login)
  allow_web_registration: true

# AuthMe
authme_login:
  # Whether to enable AuthMe login (game name or email can log in. Account cannot be unbound)
  enabled: false
  # Email domain used when AuthMe hasn't registered an email (final email: <game_name>@<domain>)
  fallback_email_domain: "authme.local"
  # External AuthMe database (use when AuthMe is on a proxy/login server, not the same server as WebMarket)
  # When enabled, does not require AuthMe plugin to be installed on this server; connects directly to remote AuthMe DB for authentication
  # Only supports MySQL/MariaDB; password algorithms support SHA256 (AuthMe default) and bcrypt
  external_database:
    enabled: false
    host: "localhost"
    port: 3306
    database: "authme"
    username: "root"
    password: ""
    table_name: "authme"          # AuthMe table name
    password_column: "password"   # Password column name
    username_column: "username"   # Username column name
    email_column: "email"         # Email column name

# ---------------The following generally do not need modification---------------

# Logging configuration
logging:
  log_market_actions: true # Whether to log market operations
  log_auth_actions: true # Whether to log authentication operations
  log_binding_actions: true # Whether to log binding/unbinding operations
  log_official_shop_actions: true # Whether to log official shop operations
  log_password_change: true # Whether to log password changes
  log_auction_actions: true # Whether to log auction operations
  log_buy_request_actions: true  # Whether to log buy request operations
  log_retention_days: 30   # Log retention days

# Cache configuration
cache:
  expire_after_write: 300 # Cache expiry time after write (seconds)
  maximum_size: 100000 # Maximum cache size

# Leaderboard configuration
leaderboard:
  fetch_interval_minutes: 10 # Leaderboard data cache/refresh interval (minutes). Requests within interval return cached results.

# PlaceholderAPI configuration
placeholderapi:
  wealth_cache_seconds: 10 # Wealth leaderboard placeholder cache time (seconds), 0 means no caching, each request triggers an async refresh

# Binding related configuration
binding:
  code_expiry_minutes: 5 # Binding code validity period (minutes)

rate_limiting:
  # Global API rate limit (e.g., 100 requests per minute)
  global:
    requests: 100
    period: 1
    unit: MINUTES
  # Rate limit for authentication endpoints (login/register)
  auth:
    requests: 5
    period: 1
    unit: MINUTES

license:
  cloud:
    # Whether to ignore HTTPS certificate errors
    ignore_ssl_errors: true

# Update checker configuration
update_checker:
  # Whether to enable update checking
  enabled: true
  # Check interval (hours)
  check_interval_hours: 48
  # Whether to notify admins of updates when they join the game
  notify_admins_on_join: true

debug:
  # Whether to enable SQL query logging (for debugging only)
  log_sql_queries: false
  # API request/response log level
  api_log_level: "INFO" # DEBUG, INFO, WARN, ERROR
```
