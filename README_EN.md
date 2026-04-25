# WebMarket

**其他语言版本: [English](README_EN.md)，[中文](README.md)。**

[Demo video](https://www.youtube.com/watch?v=tvTJZuOYvno) /
[Demo site](https://sd.kurt6.cn)

Powerful Minecraft web market plugin with a basic free edition and a full paid edition.

Supports Paper / Folia / Spigot / Bukkit / Purpur on `1.20+`.

The free edition focuses on the core web market, inventory viewing, pending claims, trade logs, account, and economy flows, with a maximum of 100 concurrent player-market listings and no points-based trading. The paid edition adds GUI, buy requests, auctions, official shop modules, buff shop, special-item / perk areas, and cross-server features.

---

## Free vs Paid

[Purchase link](https://www.patreon.com/posts/154367931)

| Feature | Free Edition | Paid Edition |
|---|---|---|
| Core global market (player market, 100 listing cap) | Yes | Yes |
| Points currency trading | No | Yes |
| Offline operations | Yes | Yes |
| In-game GUI interface | No | Yes |
| Buy request system | No | Yes |
| Auction house | No | Yes |
| Official shop sell / buyback | No | Yes |
| Buff shop | No | Yes |
| Special item / perk shop | No | Yes |
| Cross-server features | No | Yes |
| Per-player permission-group overrides | No | Yes |

---

## Highlights

- Offline support
  Players can still use the core market and inventory-related web flows while offline.

- Full NBT preservation
  Durability, enchants, potion effects, custom names, lore, shulker box contents, bundle contents, and more are preserved and displayed on the web page.

- Container listing
  Entire boxes / bundles can be listed directly, with web preview support.

- Official shop dynamic pricing (Paid)
  Dynamic pricing can adjust item prices based on recent transaction trends.

- Buff shop and special item / perk area (Paid)
  Buffs can be sold by seconds. Special items can execute one or more custom commands with variables such as `{player}`.

- Mixed modpack compatibility
  Works with vanilla, modded, hybrid-server resources, and partial custom icon sources such as ItemsAdder / CraftEngine.

---

## Modules

| Module | Edition | Description |
|---|---|---|
| Player Market | Free / Paid | Player-to-player listing and buying with configurable tax and whitelist / blacklist rules |
| Buy Requests | Paid | Players can post buy orders and let others fulfill them |
| Auction House | Paid | Auction area with configurable tax and item restrictions |
| Official Shop | Paid | Official selling area, buyback area, buff area, and special-item area |

---

## Backpack / Inventory

- View online or offline player inventory and ender chest from the web page
- Display durability, enchants, lore, and container contents
- Sell inventory or ender chest items directly to market / auction

---

## Account System

- Supports AuthMe login by player name or email
- Supports in-game registration with `/wm register <email> <password> [username]`
- Supports web registration and Minecraft account binding
- Supports API-key-based login

---

## Common Commands

All commands support the `/wm` prefix. Some also have short aliases.

| Command | Description |
|---|---|
| `/wm`, `/wm gui`, `/market` | Open the in-game market GUI |
| `/wm help` | Show available command help |
| `/wm bind <code>` | Bind web account to Minecraft account |
| `/wm register <email> <password> [username]` | Register a web account in-game |
| `/wm claim` | Claim pending items |
| `/wm sj <amount> <unit_price> [money/points]` | Quick list the held item |
| `/wm sg <amount> <unit_price> [money/points]` | Quick create a buy request |
| `/wm pm <amount> <start_price> <hours> [buyout] [money/points]` | Quick create an auction |
| `/wm sell ...` | Admin command for official shop selling area |
| `/wm recycle ...` | Admin command for official buyback area |
| `/wm buff ...` | Admin command for buff shop |
| `/wm specialitem ...` | Admin command for special-item / perk shop |
| `/wm marketlogs ...` | Query player trade logs |
| `/wm marketlogs-material ...` | Query material trade logs |
| `/wm restrict` | Restrict player access to market / buy request / auction features |
| `/wm blockitem` | Block specific NBT items from listing / auction / buy request creation |
| `/wm iconcache` | Manage generated web icon cache |

For the full command reference and parameter details, see [README.md](./README.md).

---

## Cross-Server

The `cross_server` section in `config.yml` controls cross-server behavior.

- Cross-server mode requires `MySQL`
- `isolated`: markets are separated by server
- `shared`: markets are shared across servers
- Optional item sync / economy sync / transaction sync can be configured
- Master server settings are supported for shared mode

---

## Activation

### Free Edition

- No activation code required

### Paid Edition

1. Purchase the paid edition
2. Get the activation code from the developer
3. Put the code into `activation_code` in `config.yml`

If paid-edition license validation fails, the plugin will stop instead of continuing in a downgraded mode.

---

## Configuration

The plugin uses `config.yml` as its main configuration file.

Key sections include:

- `database`
- `api`
- `web`
- `cross_server`
- `market`
- `auction`
- `official_shop`
- `offline_inventory`
- `simple_economy`
- `security`
- `authme_login`

For the full configuration example, see [README.md](./README.md) or the generated `config.yml` in the plugin resources.

---

## PlaceholderAPI

After installing `PlaceholderAPI`, the plugin registers `%webmarket_*%` placeholders such as:

- `%webmarket_balance%`
- `%webmarket_balance_formatted%`
- `%webmarket_rank%`
- `%webmarket_top_1_name%`
- `%webmarket_top_1_balance%`

---

## bStats

![bStats](https://bstats.org/signatures/bukkit/webmarket.svg)

---

## 配置文件

```yaml
activation_code: "" # License key

# Plugin language
# Available values: zh_cn, en_us
language: "en_us"

# Database settings
database:
  type: "SQLite" # SQLite or MySQL
  # MySQL settings (recommended for larger servers, requires 8.0+)
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

# API / Web server settings
api:
  enabled: true # Enable the HTTP API / Web service
  enable_on_secondary_shared_server: false # Whether secondary servers also start HTTP in shared mode; usually only the primary server needs it
  port: 8880 # Listening port
  host: "0.0.0.0" # Bind address; "0.0.0.0" listens on all network interfaces
  worker_threads: 4 # Request worker thread count
  queue_capacity: 1600 # Request queue capacity
  ssl:
    enabled: false # Enable HTTPS. When false, plain HTTP is used
    key_store_path: "ssl/keystore.p12" # Keystore path; absolute path or relative to plugins/WebMarket/
    key_store_password: "" # Keystore password
    key_password: "" # Private key password; defaults to key_store_password when empty
    key_store_type: "PKCS12" # Keystore type, for example PKCS12 / JKS
    protocol: "TLS" # SSLContext protocol, usually leave as TLS

# Player identity matching mode for bindings
player_identity:
  mode: "name" # uuid=identify by UUID (recommended for online-mode servers), name=identify by player name (recommended for offline-mode servers)

# Web frontend settings
# Custom logo icon path: plugins/WebMarket/web-assets/logo/logo.png
web:
  # Website logo text
  logo_text: 'WebMarket'
  # Prefer custom-name item images from plugins/WebMarket/web-assets/custom-images/<CustomName>.png without color codes
  # When enabled, custom named item images are used first, then fall back to material images (excluding player-renamed items)
  use_custom_name_image: true
  # Allow custom names to override the material display name; when enabled the extra "custom name" line is hidden (excluding player-renamed items)
  use_custom_name_override: true
  # Generate and cache item icons on the backend; output goes to plugins/WebMarket/web-assets/generated-icons/
  # Keeping vanilla resource download enabled is recommended
  generated_item_icons:
    enabled: true
    # Warning: enabling this can expose icon resources from custom item plugins such as CraftEngine / ItemsAdder
    # Allow generating web icons for ItemsAdder custom items
    itemsadder_enabled: false
    # Allow generating web icons for CraftEngine custom items
    craftengine_enabled: false
    # Allow extracting vanilla icons from server resources
    vanilla_enabled: true
    # When local vanilla assets are missing, try downloading and caching them from the official Minecraft client resources
    vanilla_download_enabled: true
    # Vanilla client download mirror list. Tried in order, with Mojang as the final fallback.
    # Each entry should be a base URL. Mojang/Piston paths are appended automatically.
    vanilla_download_sources:
      - "https://bmclapi2.bangbang93.com"
      - "https://launchermeta.mojang.com"
    # Allow extracting icon/model overrides from world datapacks
    datapack_enabled: true
    # Allow extracting icon assets from hybrid-server mod resources
    hybrid_mod_enabled: true
    # Output debug logs for CE/IA/resource matches
    debug_logging: false
    # Enable automatic cleanup for icon cache files
    cleanup_enabled: true
    # Max retention days for files under generated-icons. 0 disables automatic cleanup for this directory
    generated_icons_max_age_days: 0
    # Max retention days for files under vanilla-cache. 0 disables automatic cleanup for this directory
    vanilla_cache_max_age_days: 90

# Cross-server settings
cross_server:
  enabled: false # Enable cross-server support (MySQL only; automatically disabled on SQLite)
  mode: "isolated" # isolated=server-isolated data with aggregated listings, shared=fully shared across servers
  server_name: "server-1" # Unique name of this server
  server_aliases: [] # Old server-name aliases; useful after renaming server_name to keep old offline inventory / server records compatible
  master_server_name: "server-1" # Primary server name
  item_sync_enabled: false # Whether an external cross-server inventory sync solution is installed. When enabled, the plugin's offline inventory snapshot system is disabled and offline actions that require direct inventory deduction are blocked
  economy_sync_enabled: false # Whether money balance is shared across servers. In isolated mode, false means money balance and wealth leaderboards are stored per server; PlayerPoints always reads the local server value
  transaction_sync_enabled: false # Whether trade statistics are shared across servers. In isolated mode, false keeps transaction / sell / buy leaderboards separated per server
  known_servers: # Selectable server list for the web UI / GUI
    - "server-1"

# Built-in economy settings
simple_economy:
  # For cross-server setups, the built-in economy is usually the better choice
  # Enable the built-in Vault economy when no external economy plugin is installed (such as CMI / EssentialsX)
  # If enabled while an external economy plugin exists, WebMarket still uses the built-in economy
  # You may also disable CMI economy and use this plugin's economy instead
  enabled: false
  starting_balance: 100.0  # Initial balance for new players
  max_balance: 999999999.0  # Maximum balance limit
  min_transfer: 0.01  # Minimum transfer amount
  currency_singular: "Coins"  # Singular currency name
  currency_plural: "Coins"    # Plural currency name
  # Transaction history retention days (-1 = keep forever)
  transaction_history_days: 30

# Market settings
market:
  enabled: true # Global player market switch
  broadcast_create_message: true # Broadcast a clickable server-wide message when a player lists a market item
  tax_payer: "seller" # Tax payer: seller=buyer pays quoted price, buyer=buyer pays quoted price + tax
  tax_rates:
    money: 0.01 # Money trade tax rate
    points: 0.00 # Points trade tax rate (points settle as integers; non-zero tax is rounded to an integer)
  max_items_per_page: 24 # Items loaded per incremental page request
  max_listing_duration: 14 # Maximum listing duration in days
  max_listings_per_player: 10 # Maximum active listings per player
  listing_cooldown_seconds: 1 # Listing cooldown in seconds
  # Item listing restrictions
  item_restrictions:
    # Restriction mode:
    # - "none": no restriction (default)
    # - "whitelist": only listed items can be listed
    # - "blacklist": listed items cannot be listed
    mode: "none"
    # Restriction list (acts as whitelist or blacklist depending on mode)
    items:
      # Item ID format: minecraft:item_id or ITEM_ID
      - "minecraft:bedrock"
      - "minecraft:command_block"
  # Buy request settings
  buy_request:
    enabled: true # Enable buy requests
    broadcast_create_message: true # Broadcast a clickable server-wide message when a player creates a buy request
    tax_payer: "seller" # Tax payer: seller=seller receives quote - tax, buyer=seller receives quoted price
    tax_rates:
      money: 0.02 # Money buy-request trade tax rate
      points: 0.00 # Points buy-request tax rate (integer settlement; tax is rounded)
    max_quantity: 99999 # Maximum quantity allowed in a single buy request
    max_requests_per_player: 3 # Maximum active buy requests per player
    max_request_duration: 7 # Maximum request duration in days
    request_cooldown_seconds: 1 # Buy request publish cooldown in seconds
    # Buy request item restrictions
    item_restrictions:
      mode: "none" # none, whitelist, blacklist
      # Restriction list (acts as whitelist or blacklist depending on mode)
      items:
        - "minecraft:bedrock"
        - "minecraft:command_block"

# Auction settings
auction:
  enabled: true # Global auction switch
  broadcast_create_message: true # Broadcast a clickable server-wide message when a player creates an auction
  tax_payer: "seller" # Tax payer: seller=buyer pays quoted price, buyer=buyer pays quoted price + tax
  tax_rates:
    money: 0.03 # Auction money tax rate
    points: 0.00 # Auction points tax rate (integer settlement; tax is rounded)
  max_items_per_page: 24 # Items loaded per incremental page request
  max_listings_per_player: 10 # Maximum concurrent auctions per player
  listing_cooldown_seconds: 1 # Listing cooldown in seconds
  max_duration_hours: 48 # Maximum auction duration in hours
  # Auction item restrictions
  item_restrictions:
    mode: "none" # none, whitelist, blacklist
    # Restriction list (acts as whitelist or blacklist depending on mode)
    items:
      # Item ID format: minecraft:item_id or ITEM_ID
      - "minecraft:bedrock"
      - "minecraft:command_block"

# Offline inventory settings
offline_inventory:
  enabled: true  # Enable offline inventory support
  ender_chest_display_enabled: true # Show ender chest items at the bottom of the web inventory page
  ender_chest_offline_enabled: true # Enable ender chest offline snapshot display / offline sell / offline auction

# Official shop settings
official_shop:
  # Dynamic pricing settings
  dynamic_pricing:
    # Enable the dynamic pricing system
    # Uses a 3-day weighted average and a sigmoid curve to smooth changes
    # Dynamic price = base price × (1 + sigmoid(3-day trend) × sensitivity × trend weight)
    enabled: true

    # Price reset strategy
    # false: never reset (price keeps changing with trade volume)
    # daily: reset to base price on the first check after 00:00 each day
    # weekly: reset to base price every Monday
    # monthly: reset to base price on the first day of each month
    restart: false

    # Trade activity algorithm settings
    activity:
      # Sensitivity (0.01-1.0)
      # Higher values make price changes react more strongly to trade volume
      # Recommended: 0.05-0.2
      sensitivity: 0.1

      # Daily trade volume threshold
      # Price movement starts only when today's trade volume reaches this value
      # Helps avoid extreme swings from very small numbers of trades; 1-10 is recommended
      daily_volume_threshold: 1

    # Global price guard rails
    price_protection:
      # Enable a minimum price floor
      enable_floor: true

      # Minimum price multiplier relative to the base price
      # The algorithm also adjusts dynamically based on price volatility:
      # - High volatility (>30%): limited to 0.7x-1.5x of base price
      # - Medium volatility (>10%): limited to 0.5x-2.0x of base price
      # - Low volatility: uses the configured multiplier directly
      min_price_multiplier: 0.5

      # Enable a maximum price ceiling
      enable_ceiling: true

      # Maximum price multiplier relative to the base price
      # Also adjusted dynamically based on volatility
      max_price_multiplier: 2.0

# Item-related settings
items:
  # Check the item's maximum stack size
  max_stack_size_check: true
  # Minimum quantity allowed in a single listing
  min_quantity: 1
  # Maximum quantity allowed in a single listing
  max_quantity: 2304
  # Price limits
  min_price: 0.01
  max_price: 10000000.0

security:
  # Default API key validity period in days
  api_key_expiry_days: 7
  # Password encryption cost (iterations). Higher is more secure but slower
  encryption_iterations: 10000
  # Enable email domain whitelist (only allowed domains can register)
  email_whitelist_enabled: false
  # Allowed email domains (domain only, without @)
  # Example: ["qq.com", "gmail.com"]
  email_whitelist_domains:
    - "qq.com"
  # Registration limit per IP (0 = unlimited)
  registration_limit_per_ip: 2
  # Allow registration through the Web form. When disabled, users must register/login through AuthMe
  allow_web_registration: true

# AuthMe
authme_login:
  # Enable AuthMe login (players can log in with either name or email; account unbinding is not allowed)
  enabled: false
  # Email domain used when AuthMe has no registered email (final email: <player>@<domain>)
  fallback_email_domain: "authme.local"
  # External AuthMe database (use this when AuthMe runs on a proxy/login server instead of this server)
  # When enabled, AuthMe does not need to be installed locally; authentication is done directly against the remote AuthMe database
  # MySQL/MariaDB only; password algorithms supported: SHA256 (AuthMe default) and bcrypt
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

# ---------------Usually no changes needed below---------------

# Logging settings
logging:
  log_market_actions: true # Log market actions
  log_auth_actions: true # Log authentication actions
  log_binding_actions: true # Log binding / unbinding actions
  log_official_shop_actions: true # Log official shop actions
  log_password_change: true # Log password changes
  log_auction_actions: true # Log auction actions
  log_buy_request_actions: true  # Log buy request actions
  log_retention_days: 30   # Log retention period in days

# Cache settings
cache:
  expire_after_write: 300 # Cache expiration after write in seconds
  maximum_size: 100000 # Maximum cache entry count

# Leaderboard settings
leaderboard:
  fetch_interval_minutes: 10 # Leaderboard cache / refresh interval in minutes; repeated requests within the interval return cached data

# PlaceholderAPI settings
placeholderapi:
  wealth_cache_seconds: 10 # Wealth placeholder cache duration in seconds; 0 means no retained cache and every request triggers an async refresh

# Binding settings
binding:
  code_expiry_minutes: 5 # Binding code validity period in minutes

rate_limiting:
  # Global API rate limit (for example: 100 requests per minute)
  global:
    requests: 100
    period: 1
    unit: MINUTES
  # Rate limit for authentication endpoints (login / register)
  auth:
    requests: 5
    period: 1
    unit: MINUTES

license:
  cloud:
    # Ignore HTTPS certificate validation
    ignore_ssl_errors: true

# Update checker settings
update_checker:
  # Enable update checking
  enabled: true
  # Check interval in hours
  check_interval_hours: 48
  # Notify admins about updates when they join
  notify_admins_on_join: true

debug:
  # Log SQL queries (debug only)
  log_sql_queries: false
  # API request/response log level
  api_log_level: "INFO" # DEBUG, INFO, WARN, ERROR
```
