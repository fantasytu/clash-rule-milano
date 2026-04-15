# clash-rule-milano

OpenClash 订阅转换模板（Milano 定制版），基于 [Aethersailor/Custom_OpenClash_Rules](https://github.com/Aethersailor/Custom_OpenClash_Rules) 魔改，增加了软件包管理器分组，并将 YAML 规则文件收录至本仓库自托管。

## 使用方法

在 OpenClash 订阅转换中，模板 URL 填入：

```
https://testingcf.jsdelivr.net/gh/fantasytu/clash-rule-milano@main/Milano.ini
```

## 与原版的主要差异

| 改动 | 说明 |
|------|------|
| `category-communication` → `category-communication-!cn` | 即时通讯分组明确排除中国服务，与其他 `!cn` 规则保持一致 |
| 新增 `📦 软件源` 分组 | 覆盖 Homebrew / apt / npm / pip / Cargo / Go / Maven / Docker 等包管理器 |
| 新增 `category-dev-cn` 直连规则 | 国内镜像站（阿里云镜像、清华源等）直连，不走代理 |
| YAML 规则文件自托管 | 原 Aethersailor 的 YAML 文件下载至 `rule/` 目录，URL 指向本仓库 |

---

## 规则分组说明

### 直连分组

| 规则 | 来源 | 说明 |
|------|------|------|
| `GEOSITE,private` | v2fly | 本地地址、局域网域名 |
| `GEOIP,private` | v2fly | 本地/保留 IP 段 |
| `GEOSITE,google-cn` | v2fly | 谷歌在国内可用的域名 |
| `GEOSITE,category-games@cn` | v2fly | 国内游戏域名 |
| `GEOSITE,category-game-platforms-download` | v2fly | 各大游戏平台下载域名 |
| `GEOSITE,category-public-tracker` | v2fly | BT Tracker 域名 |
| `GEOSITE,category-dev-cn` | v2fly | 国内开发者镜像源（阿里云镜像、清华源等） |
| `GEOSITE,cn` | v2fly | 国内域名兜底白名单 |
| `GEOIP,cn` | Loyalsoldier | 国内 IP 兜底 |

### 代理分组

| 分组 | 规则来源 | 覆盖内容 |
|------|----------|----------|
| 💬 即时通讯 | `GEOSITE,category-communication-!cn` + `GEOIP,telegram` | Telegram、WhatsApp、Signal、Discord、Line 等 |
| 🌐 社交媒体 | `GEOSITE,category-social-media-!cn` + `GEOIP,twitter/facebook` | Twitter(X)、Facebook、Instagram 等 |
| 🤖 ChatGPT | `GEOSITE,openai` | OpenAI / ChatGPT |
| 🤖 Copilot | `GEOSITE,bing` | Bing / Copilot |
| 🤖 Claude | 自定义 YAML | Claude AI 服务 |
| 🤖 AI服务 | `GEOSITE,category-ai-!cn` | 其他 AI 服务 |
| 🚀 GitHub | `GEOSITE,github` | GitHub |
| 📦 软件源 | 见下方详细说明 | 包管理器 / 容器镜像源 |
| 📹 YouTube | `GEOSITE,youtube` | YouTube |
| 🎥 Netflix | `GEOSITE,netflix` + `GEOIP,netflix` | Netflix |
| 🎥 DisneyPlus | `GEOSITE,disney` | Disney+ |
| 🎥 HBO | `GEOSITE,hbo` | HBO Max |
| 🎥 PrimeVideo | `GEOSITE,primevideo` | Amazon Prime Video |
| 🎥 AppleTV+ | `GEOSITE,apple-tvplus` | Apple TV+ |
| 🎥 Emby | `GEOSITE,category-emby` | Emby 服务 |
| 🎶 TikTok | `GEOSITE,tiktok` | TikTok |
| 🎻 Spotify | `GEOSITE,spotify` | Spotify |
| 📺 Bahamut | `GEOSITE,bahamut` | 巴哈姆特（台湾节点） |
| 🎮 Steam | `GEOSITE,steam` | Steam 商店 |
| 🎮 游戏平台 | `GEOSITE,category-games` | 海外游戏平台 |
| 🌎 国外媒体 | `GEOSITE,category-entertainment` | 海外综合媒体 |
| 💾 OneDrive | `GEOSITE,onedrive` | OneDrive |
| Ⓜ️ 微软服务 | `GEOSITE,microsoft` | Microsoft |
| 🇬 谷歌服务 | `GEOSITE,google` + `GEOIP,google` | Google |
| 📢 谷歌FCM | `GEOSITE,googlefcm` | Firebase Cloud Messaging |
| 🍎 苹果服务 | `GEOSITE,apple` | Apple |
| 💳 PayPal | `GEOSITE,paypal` | PayPal |
| 🛒 国外电商 | `GEOSITE,category-ecommerce` | 海外电商 |
| ⏬ PT站点 | `GEOSITE,category-pt` | PT 私有追踪器 |
| 🚀 测速工具 | `GEOSITE,category-speedtest` | SpeedTest 等测速工具 |
| 🚀 手动选择 | 自定义 YAML + `GEOSITE,gfw` | 代理兜底 |
| 🐟 漏网之鱼 | `FINAL` | 最终兜底 |

### 📦 软件源 — 详细规则

| 规则 | 覆盖的包管理器 / 服务 |
|------|----------------------|
| `GEOSITE,category-dev-cn`（**直连**） | 阿里云镜像、清华 TUNA、中科大 USTC、华为云镜像等国内开发者镜像站 |
| `GEOSITE,category-dev` | **Homebrew**（brew.sh）、**apt/Ubuntu/Debian/Arch/Fedora/CentOS** 等 Linux 发行版官方源、**npm/Node.js**（nodesource.com）、**pip/PyPI**（pypi.org）、**Cargo/Rust**（crates.io）、**Go modules**（proxy.golang.org）、**Maven/Gradle**（maven.apache.org）、**RubyGems**（rubygems.org）、**Composer/PHP**、**Docker**、**Kubernetes**、**Flatpak** 等 |
| `GEOSITE,category-container` | **Docker Hub**（docker.io）、**GHCR**（ghcr.io）、**GCR**（gcr.io）、**ECR**（ecr.aws / *.dkr.ecr.*.amazonaws.com）、**MCR**（mcr.microsoft.com）、**Quay**（quay.io）、**GitLab Registry**（registry.gitlab.com）、**registry.k8s.io** 等容器镜像仓库 |
| `GEOSITE,npmjs` | **npm registry**（registry.npmjs.org、npmjs.com） |

---

## 数据来源

### GeoSite 数据

GeoSite 规则由以下项目提供，通过 OpenClash 内置的 `geosite.dat` 文件生效：

- **[v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)**：GeoSite 原始域名数据，按分类维护，`category-*` 系列均来自此项目
- **[Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)**：在 v2fly 基础上增强的 `geosite.dat` 和 `geoip.dat`，OpenClash 默认使用此版本

#### `!cn` 变体说明

带 `!cn` 后缀的 GeoSite 类别（如 `category-communication-!cn`、`category-social-media-!cn`）表示**排除所有打了 `@cn` 标签的条目**，即仅保留非中国服务。适合用于需要走代理的分组，避免国内服务被误代理。

#### 主要 GeoSite 分类

| 分类名 | 说明 |
|--------|------|
| `category-communication` | 即时通讯（Telegram、WhatsApp、Signal、Discord、Line 等） |
| `category-communication-!cn` | 同上，明确排除中国服务 |
| `category-social-media-!cn` | 海外社交媒体（Twitter/X、Facebook、Instagram 等） |
| `category-dev` | 开发者工具、包管理器、Linux 发行版源（见上方详细列表） |
| `category-dev-cn` | 国内开发者镜像站 |
| `category-container` | 容器镜像仓库（Docker Hub、GHCR、GCR 等） |
| `category-ai-!cn` | 海外 AI 服务 |
| `category-games` | 海外游戏平台 |
| `category-games@cn` | 国内可用的游戏域名 |
| `category-game-platforms-download` | 游戏平台下载域名（直连加速） |
| `category-entertainment` | 海外综合媒体娱乐 |
| `category-emby` | Emby 媒体服务 |
| `category-ecommerce` | 海外电商 |
| `category-pt` | PT 私有追踪器 |
| `category-speedtest` | 网络测速工具 |
| `category-public-tracker` | BT 公共 Tracker |
| `gfw` | GFWList 被封锁域名 |
| `cn` | 中国大陆域名白名单 |

### GeoIP 数据

| 分类 | 来源 | 说明 |
|------|------|------|
| `GEOIP,private` | v2fly | 私有/保留 IP 段（RFC1918 等） |
| `GEOIP,telegram` | Loyalsoldier | Telegram IP 段 |
| `GEOIP,twitter` | Loyalsoldier | Twitter IP 段 |
| `GEOIP,facebook` | Loyalsoldier | Facebook IP 段 |
| `GEOIP,google` | Loyalsoldier | Google IP 段 |
| `GEOIP,netflix` | Loyalsoldier | Netflix IP 段 |
| `GEOIP,cn` | Loyalsoldier | 中国大陆 IP 段（CNIP） |

### 自托管 YAML 规则文件

#### 来源于 Aethersailor/Custom_OpenClash_Rules
以下文件来源于 Aethersailor/Custom_OpenClash_Rules，已下载至本仓库 `rule/` 目录，URL 指向本仓库，避免依赖上游变更：

| 文件 | 类型 | 说明 |
|------|------|------|
| `Custom_Direct_Domain.yaml` | clash-domain | 自定义直连域名 |
| `Custom_Direct_Classical_IP.yaml` | clash-classic | 自定义直连 IP/域名 |
| `Custom_Proxy_Domain.yaml` | clash-domain | 自定义代理域名 |
| `Custom_Proxy_Classical_IP.yaml` | clash-classic | 自定义代理 IP/域名 |
| `Custom_Port_Direct.yaml` | clash-classic | 非标端口直连规则 |

#### 本仓库新增
以下文件为本仓库新增：

| 文件 | 类型 | 说明 |
|------|------|------|
| `Claude.yaml` | clash-classic | Claude AI 服务规则 |
| `Steam.yaml` | clash-classic | Steam 服务规则 |
| `Steam_CDN_Classical.yaml` | clash-classic | Steam CDN 直连节点 |
| `Telegram.yaml` | clash-classic | Telegram 服务规则 |
| `PlayStation.yaml` | clash-classic | PlayStation 服务规则 |
| `PlayStationNetwork.yaml` | clash-classic | PlayStation Network 服务规则 |

---

## 致谢

- [Aethersailor/Custom_OpenClash_Rules](https://github.com/Aethersailor/Custom_OpenClash_Rules) — 原始模板
- [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community) — GeoSite 域名数据
- [Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat) — 增强版 geosite.dat / geoip.dat
