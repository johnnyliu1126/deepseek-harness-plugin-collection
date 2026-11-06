# DeepSeek Harness 额外插件合集

[English](README.md) | [简体中文](README.zh-CN.md) | [Downloads / 下载](https://github.com/johnnyliu1126/deepseek-harness-plugin-collection/releases/tag/v0.1.0)

把本机额外安装和维护的 DeepSeek Harness 插件整理到一个仓库，方便了解功能、按需安装，以及换机后恢复插件环境。

本仓库记录 **19 个插件条目、12 个顶层安装项、72 条功能说明**，其中两个本地插件提供源码。DeepSeek Harness 自带插件不上传；第三方插件保留原作者与上游地址，安装时从固定版本来源下载并校验。

## 按平台选择仓库

| Platform / 平台 | Repository / 仓库 |
|---|---|
| Mac Intel / x64 | [deepseek-harness-plugins-macos-intel](https://github.com/johnnyliu1126/deepseek-harness-plugins-macos-intel) |
| Mac M 系列 / arm64 | [deepseek-harness-plugins-macos-apple-silicon](https://github.com/johnnyliu1126/deepseek-harness-plugins-macos-apple-silicon) |
| Windows / x64 | [deepseek-harness-plugins-windows](https://github.com/johnnyliu1126/deepseek-harness-plugins-windows) |

Each edition has native architecture checks and its own CI. / 每版有独立架构检查与对应平台 CI。Windows 版排除 macOS 重启插件。

## 先看这里

- 想知道装了什么：看下面的插件表。
- 想知道具体怎么用：看“逐插件功能与用法”，或点击插件名查看详细文档。
- 想直接安装：看“安装与启动”，可以只装指定插件。
- 想下载压缩包：打开 [v0.1.0 预发布版](https://github.com/johnnyliu1126/deepseek-harness-plugin-collection/releases/tag/v0.1.0)，含源码 ZIP、两个本地插件 TGZ 和 SHA256SUMS。

**兼容性须知：** 当前模板默认禁用任务看板、宠物、图像描述和皮肤中心；手机插件存在 React peer 版本不匹配。已安装、已声明与实际功能可用是不同状态，详见文末验证说明。

## 有哪些插件

### 12 个顶层安装项

| 插件 | 版本 | 主要用途 | 怎么开始 |
|---|---|---|---|
| [dsh-purge-community](catalog/dsh-purge-community/README.zh-CN.md) | 1.6.60 | 状态、规则与补丁管理 | 打开插件侧栏，先看状态自检和备份，再按需管理预设提示词、规则或执行回滚。 |
| [@neystan/dsh-web-ui-all](catalog/neystan--dsh-web-ui-all/README.zh-CN.md) | 0.1.16 | Web UI 全家桶 | 安装聚合包后使用对应看板、Git 图、右侧文件面板等入口；四个兼容性受限子项默认禁用。 |
| [dsh-lark-channel](catalog/dsh-lark-channel/README.zh-CN.md) | 0.0.7 | 飞书 / Lark 机器人 | 先配置飞书/Lark 机器人和本地凭据，再向机器人发任务；用 /status、/ws、/cd、/model、/sessions 管理会话。 |
| [@tt-a1i/archify-dsh](catalog/tt-a1i--archify-dsh/README.zh-CN.md) | 1.0.0 | 架构图 | 在对话里说：“使用 archify skill 分析当前仓库，生成架构 JSON 和 HTML，并告诉我文件路径。” |
| [dsh-prompt-enhancer](catalog/dsh-prompt-enhancer/README.zh-CN.md) | 1.2.2 | 提示词优化 | 在输入框写草稿，点击“优化”，检查改写内容后再发送；设置中可选精简、均衡、详细或自定义。 |
| [@liustack/modlens](catalog/liustack--modlens/README.zh-CN.md) | 3.27.2 | 图像理解与 OCR | 先配置视觉提供商，再说：“读取这张图片，提取全部文字并解释图表。”遇到问题运行 modlens doctor。 |
| [@liustack/modsearch](catalog/liustack--modsearch/README.zh-CN.md) | 5.10.11 | 网页与 X 搜索 | 在对话中要求搜索或抓取，例如：“搜索这个技术问题，并附上来源链接。”X 搜索还需要已配置的 Grok Build。 |
| [dsh-ego-browser](catalog/dsh-ego-browser/README.zh-CN.md) | 0.9.8 | 浏览器自动化 | 让 Agent 打开网页并执行交互，在右侧面板观察过程；需要登录时按插件流程导入或手工登录。 |
| [dsh-client-liang-intensity-skin](catalog/dsh-client-liang-intensity-skin/README.zh-CN.md) | 0.1.6 | 推理滑块与皮肤 | 在外观设置启用皮肤，选择支持多个 reasoning effort 的模型，拖动并松开滑块提交档位。 |
| [dsh-restart](catalog/dsh-restart/README.zh-CN.md) | 1.0.0 | 一键重启 | 在 macOS Desktop 侧栏页脚点击“重启”；先保存工作，真实重启会中断正在执行的任务。 |
| [dsh-balance-monitor](catalog/dsh-balance-monitor/README.zh-CN.md) | 1.0.0 | 余额监控 | 先登录宿主 DeepSeek 账号并打开一个会话；在输入框下方查看余额，点击余额展开刷新间隔和阈值。 |
| [dsh-mobile](catalog/dsh-mobile/README.zh-CN.md) | 0.8.2 | 手机访问 | 在手机访问设置选择 LAN 或远程方式，手机扫码配对；账号、隧道和通知权限在本机单独配置。 |

### Web UI 聚合包内的 7 个子插件

安装 `@neystan/dsh-web-ui-all` 会拉取这些子包，不必重复安装。只需要其中一项时，可以改装子插件。**不要同时选择聚合包与同一子插件。**

| 子插件 | 功能 | 本合集默认状态 |
|---|---|---|
| [@neystan/dsh-client-ui-task-board](catalog/neystan--dsh-client-ui-task-board/README.zh-CN.md) | 任务看板、定时任务与待办 | 禁用，需升级宿主并复测 |
| [@neystan/dsh-client-ui-aionui-panel](catalog/neystan--dsh-client-ui-aionui-panel/README.zh-CN.md) | 文件树与多标签预览 | 未额外禁用；运行兼容性仍需确认 |
| [@neystan/dsh-client-ui-git-graph](catalog/neystan--dsh-client-ui-git-graph/README.zh-CN.md) | Git 图与分支管理 | 未额外禁用；运行兼容性仍需确认 |
| [@neystan/dsh-pet](catalog/neystan--dsh-pet/README.zh-CN.md) | 宠物互动 | 禁用，需升级宿主并复测 |
| [@neystan/dsh-skins](catalog/neystan--dsh-skins/README.zh-CN.md) | 皮肤合集 | 未额外禁用；运行兼容性仍需确认 |
| [@neystan/dsh-tool-describe-image](catalog/neystan--dsh-tool-describe-image/README.zh-CN.md) | 图像描述工具 | 禁用，需升级宿主并复测 |
| [@neystan/dsh-client-ui-skin-center](catalog/neystan--dsh-client-ui-skin-center/README.zh-CN.md) | 皮肤中心 | 禁用，需升级宿主并复测 |

## 安装与启动

### 1. 准备环境

需要已安装的 DeepSeek Harness、Python 3.10+、Node.js 22.19+（推荐 24）和 pnpm。本仓库盘点的宿主组件版本为 `0.2.1-rc.4`；其他版本请核对各插件兼容要求。

### 2. 克隆仓库

```sh
git clone https://github.com/johnnyliu1126/deepseek-harness-plugin-collection.git
cd deepseek-harness-plugin-collection
```

### 3. 先预览，再安装

下面的 `collection` 是新 Profile，已有目标目录会被拒绝，不会覆盖你现在使用的 `desktop` 配置。

```sh
# Preview only / 只读预览
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --all

# Create profile, verify downloads and install / 创建、校验并安装
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --all --apply --fetch
```

只需要部分插件时，用 `--plugins` 代替 `--all`。下面示例创建另一个新 Profile，只安装两个本地插件：

```sh
python3 scripts/collection.py \
  --target "$HOME/.dsh/profiles/collection-local" \
  --plugins dsh-restart dsh-balance-monitor \
  --apply --fetch
```

参数含义：`--all` 选择 12 个顶层插件；`--plugins` 选择指定包；`--apply` 创建新目录；`--fetch` 下载依赖并安装。不加 `--apply` 只输出计划。安装器默认禁用依赖生命周期脚本，且不会自动重启应用、登录账号或创建隧道。

### 4. 检查并启动新 Profile

如果有 `dsh` CLI：

```sh
dsh --profile collection --dump-config
dsh --profile collection --help
dsh --profile collection
```

安装到 `collection` 不会自动切换 Desktop 的活动 Profile。单独启动 Web 实例前，从 `--help` 查看端口选项，避免与现有实例冲突。macOS Desktop 没有 PATH 命令时，可参照 [安装指南](docs/INSTALL.zh-CN.md) 使用匹配宿主的内置 CLI。

### 5. 把单个插件装到已有 Profile

先备份当前 Profile，再使用宿主插件管理器。例如把提示词优化插件装进 `desktop`：

```sh
dsh plugin --profile desktop add dsh-prompt-enhancer@1.2.2
```

本地插件可用 `dsh plugin --profile desktop add link:/仓库绝对路径/plugins/dsh-balance-monitor`。包依赖和 bundle 由插件管理器注册；不要整份替换现有 package.json。应用是否需要重启以对应插件和宿主的提示为准。

## 逐插件功能与用法

以下 72 条功能说明来自固定版本源码、清单或随包文档。它们说明实现与使用入口，不代表所有外部服务和 UI 都已端到端验证。

### 状态、规则与补丁管理 — `dsh-purge-community`

- 状态自检与宿主证据：面板检查补丁和运行状态，失败读取不等于未安装。
- 提示词与规则：按预设管理文本、追加顺序、排除预设和一次性注入选项。
- 补丁生命周期：本机备份、应用、回滚与版本管理；可能改写宿主，需单独操作。
- 演练台：附带预设、技能、SQLite 事实库和 /redteam/api 桥接。
- 重试与继续：配置自动重试、次数上限和继续文本；不保证任务一定成功。

**使用：** 打开插件侧栏，先看状态自检和备份，再按需管理预设提示词、规则或执行回滚。

**常用设置：** `autoApplyOnStart / autoUpdateOnStart` = `false`; `autoRetry / retryMax` = `true / 3`; `autoContinue / continueMax` = `false / 3`; `postPrompt` = `empty`

[详细安装、配置、作者与限制](catalog/dsh-purge-community/README.zh-CN.md)。

### Web UI 全家桶 — `@neystan/dsh-web-ui-all`

- 聚合安装：一次安装任务看板、Git 图、右侧面板、宠物、图像描述和皮肤包。
- 组合层：通过 bundle patch 注册子插件，单独安装子包可选取部分功能。
- 兼容性：部分设置使用较新 keyed slot，本机已禁用四个不兼容子项。

**使用：** 安装聚合包后使用对应看板、Git 图、右侧文件面板等入口；四个兼容性受限子项默认禁用。

[详细安装、配置、作者与限制](catalog/neystan--dsh-web-ui-all/README.zh-CN.md)。

### 飞书 / Lark 机器人 — `dsh-lark-channel`

- 聊天驱动 Agent：飞书/Lark 文本触发真实宿主任务，推理、工具和结果分开展示。
- 持久会话：按聊天、话题或发送者隔离，/new 新建，/sessions 续接。
- 工作区和模型：/ws、/cd、/model 切换，/status 查看状态，/stop 停止。
- 交互卡片：回答模型问题、评审计划和批准工具；权限调整仍遵守批准者配置。
- 多机器人：独立凭据与会话，botPeers 限制对话对象，botHops 限制循环。
- 文件传输：接收文件到工作区；群聊发送需要逐次批准，默认单文件 20 MiB。

**使用：** 先配置飞书/Lark 机器人和本地凭据，再向机器人发任务；用 /status、/ws、/cd、/model、/sessions 管理会话。

**常用设置：** `sessionScope` = `see upstream schema`; `botHops` = `6`; `attachImages` = `false`; `receiveFiles / sendFiles` = `true`; `maxReceiveFileBytes / maxSendFileBytes` = `20 MiB`

[详细安装、配置、作者与限制](catalog/dsh-lark-channel/README.zh-CN.md)。

### 架构图 — `@tt-a1i/archify-dsh`

- 架构图技能：通过文件系统 skill provider 提供 Archify，按名称调用。
- 结构化产物：生成规范 JSON 与 HTML 图，用组件、主路径和信任边界解释仓库。
- 轻量适配：不添加模型工具或 Web UI；内置 Archify 3.0.1，与适配器版本分开。

**使用：** 在对话里说：“使用 archify skill 分析当前仓库，生成架构 JSON 和 HTML，并告诉我文件路径。”

**常用设置：** `archify-plugin` = `packaged skills root`

[详细安装、配置、作者与限制](catalog/tt-a1i--archify-dsh/README.zh-CN.md)。

### 提示词优化 — `dsh-prompt-enhancer`

- 草稿优化：输入框按钮替换草稿，保留发送前编辑和撤销的机会。
- 四档指令：精简、均衡（默认）、详细和自定义；短闲聊有防过度扩写重试。
- 模型路由：免费通道、当前模型或固定模型；免费通道失败可能回退到付费对话模型。
- 连通性与记录：设置页测试通道并显示上次实际调用；本机 settings.json 保存设置。

**使用：** 在输入框写草稿，点击“优化”，检查改写内容后再发送；设置中可选精简、均衡、详细或自定义。

**常用设置：** `mode` = `balanced`; `DSH_FREE_CHANNEL_BASE_URL` = `upstream default`; `DSH_FREE_CHANNEL_API_KEY` = `unset`; `DSH_FREE_CHANNEL_MODEL` = `upstream default`

免费通道不可用时可能回退到当前对话模型，并消耗该模型的额度；不要把“优化”理解为所有模式永远免费。

[详细安装、配置、作者与限制](catalog/dsh-prompt-enhancer/README.zh-CN.md)。

### 图像理解与 OCR — `@liustack/modlens`

- 图像理解：为文本模型补充 OCR、阅读顺序、区域、实体和关系描述。
- 多提供商：Gemini、OpenAI 兼容、Anthropic、Antigravity、Claude 和 Kimi CLI。
- 故障转移与轮换：授权、限流和额度错误可触发同提供商密钥轮换及链路回退。
- 复用现有 CLI：doctor 检测已装工具，按授权配置复用；可能消耗对应订阅额度。

**使用：** 先配置视觉提供商，再说：“读取这张图片，提取全部文字并解释图表。”遇到问题运行 modlens doctor。

[详细安装、配置、作者与限制](catalog/liustack--modlens/README.zh-CN.md)。

### 网页与 X 搜索 — `@liustack/modsearch`

- 网页搜索与抓取：给没有原生联网能力的模型提供搜索与页面正文。
- 多引擎：Firecrawl、Keenable、You.com、Antigravity、Tavily、Exa 和本地抓取。
- X 搜索：配置并登录 Grok Build 后使用对应渠道。
- 回退与密钥轮换：渠道失败时切换；免费额度是上游声明，可能变化。

**使用：** 在对话中要求搜索或抓取，例如：“搜索这个技术问题，并附上来源链接。”X 搜索还需要已配置的 Grok Build。

[详细安装、配置、作者与限制](catalog/liustack--modsearch/README.zh-CN.md)。

### 浏览器自动化 — `dsh-ego-browser`

- 浏览器工具：ego_* 工具驱动内置 ego-lite，执行页面访问和交互。
- 实时面板：SSE 画面、直接鼠标操作、标签页、下载捕获及人工验证提示。
- 登录导入：Chrome/Edge 扩展桥或非破坏性配置副本，登录资料不进入仓库。
- 不同宿主：Web 右侧栏、可选 TUI 文本面板，headless 仅工具模式。

**使用：** 让 Agent 打开网页并执行交互，在右侧面板观察过程；需要登录时按插件流程导入或手工登录。

**常用设置：** `chromePath` = `auto-detect`; `defaultSpace` = `empty`

[35 个浏览器工具逐项说明](docs/BROWSER-TOOLS.md)。

[详细安装、配置、作者与限制](catalog/dsh-ego-browser/README.zh-CN.md)。

### 推理滑块与皮肤 — `dsh-client-liang-intensity-skin`

- 推理滑块：读取模型实际 reasoning.efforts，均匀映射到 0–30。
- 提交规则：拖动仅预览，松开、键盘完成或失焦后吸附并提交原始 effort ID。
- 可见性：不支持推理、单档位或 addressed subagent 时隐藏。
- 外观切换：皮肤模式显示人物、背景和配色；原生模式恢复宿主界面。

**使用：** 在外观设置启用皮肤，选择支持多个 reasoning effort 的模型，拖动并松开滑块提交档位。

**常用设置：** `appearance` = `user-selected`

[详细安装、配置、作者与限制](catalog/dsh-client-liang-intensity-skin/README.zh-CN.md)。

### 一键重启 — `dsh-restart`

- 常驻入口：侧边栏页脚文字按钮，窄栏降级为图标。
- 重启过程：POST 路由调用 detached shell，延迟退出整棵应用进程并重新打开。
- 状态与日志：state 和 log 接口，dryRun 预演和 10 秒重复请求去抖。
- 重连：浏览器轮询宿主返回后刷新；实际重启会打断进行中的任务。

**使用：** 在 macOS Desktop 侧栏页脚点击“重启”；先保存工作，真实重启会中断正在执行的任务。

**常用设置：** `DSH_RESTART_APP_PATH` = `/Applications/DeepSeek Harness.app`; `DSH_RESTART_DELAY_MS` = `700`; `DSH_RESTART_DRY_RUN` = `0`; `debounce` = `10000 ms`

[详细安装、配置、作者与限制](catalog/dsh-restart/README.zh-CN.md)。

### 余额监控 — `dsh-balance-monitor`

- 余额：通过宿主 deepseekAccount 查询，按币种展示充值、赠金和合计。
- 刷新：默认 60 秒，可选 30/60/120/300 秒，手动刷新、请求合并和 3 秒节流。
- 提醒：低余额阈值默认 10，金额着色，设置保存在 localStorage。
- 时段：北京时间工作日时段与切换倒计时，硬编码 2026 假日。不是官方实时价格源。
- 错误状态：区分未登录、接口不可用和查询失败；失败不显示零余额。

**使用：** 先登录宿主 DeepSeek 账号并打开一个会话；在输入框下方查看余额，点击余额展开刷新间隔和阈值。

**常用设置：** `刷新间隔 / interval` = `60 s`; `低余额阈值 / threshold` = `10`

仅支持宿主账号服务；没有 API Key 查询、历史消费或会话费用估算。时段与 2026 日历是插件本地算法，不是官方实时价格源。

[详细安装、配置、作者与限制](catalog/dsh-balance-monitor/README.zh-CN.md)。

### 手机访问 — `dsh-mobile`

- 手机会话：与桌面共享 Workspace、消息和工具，适配触屏输入框、抽屉和问答卡片。
- 客户端：Android App 与手机浏览器/PWA；界面与设备列表可定制。
- 配对：二维码、链接或密钥，多设备可达性检查、切换、重新配对和移除记录。
- 网络：LAN、Tailscale、cpolar、Cloudflare、FRP、自建代理、Caddy；iroh 是平台受限实验项。
- 通知：iOS 主屏幕 Web Push 和 Android 原生通知，需用户显式开启。
- 诊断与安全：脱敏连接报告、设备凭据、Origin 绑定和第三方 WebSocket 逐路径批准。

**使用：** 在手机访问设置选择 LAN 或远程方式，手机扫码配对；账号、隧道和通知权限在本机单独配置。

**常用设置：** `pairing / network` = `configure in plugin UI`; `notifications` = `explicit opt-in`

已观察到 React 版本警告：此包要求 `^19.3.0`，隔离安装解析到 `18.3.1`。安装成功不等于手机 UI 已通过兼容验证。

[详细安装、配置、作者与限制](catalog/dsh-mobile/README.zh-CN.md)。

### 任务看板、定时任务与待办 — `@neystan/dsh-client-ui-task-board`

- 任务看板：多列卡片、宿主持久化和真实 Agent 会话执行。
- 定时任务：宿主 cron，创建、列表、暂停、恢复、运行和删除。
- 待办：添加、查询、完成和删除，数据持久保存。

**使用：** 兼容宿主上打开任务看板，添加任务或待办，为需要自动执行的任务设置 cron。当前模板默认禁用。

**当前模板禁用此项。** 先确认目标宿主支持所需 API，再单独启用与验证。

[详细安装、配置、作者与限制](catalog/neystan--dsh-client-ui-task-board/README.zh-CN.md)。

### 文件树与多标签预览 — `@neystan/dsh-client-ui-aionui-panel`

- 文件管理：Workspace 文件树、文件名搜索与 Git 改动。
- 预览：多标签查看十余种文件格式，通过宿主 fs/git 服务获取数据。

**使用：** 打开右侧文件面板，浏览工作区文件树、搜索文件名、查看 Git 改动并打开预览标签。

[详细安装、配置、作者与限制](catalog/neystan--dsh-client-ui-aionui-panel/README.zh-CN.md)。

### Git 图与分支管理 — `@neystan/dsh-client-ui-git-graph`

- 分支与图：会话顶部的分支选择器和提交关系图。
- 真实 Git 操作：通过宿主创建或切换分支，并执行操作前检查。

**使用：** 在会话顶部查看 Git 图，选择、创建或切换工作区仓库的分支；操作会影响真实 Git 状态。

[详细安装、配置、作者与限制](catalog/neystan--dsh-client-ui-git-graph/README.zh-CN.md)。

### 宠物互动 — `@neystan/dsh-pet`

- 活动动画：会话与工具事件驱动九种动画状态。
- 互动：抚摸、喂食、亲密度和鱼干库存，宿主统一保存。
- 自定义：分别导入 pet.json 与 spritesheet.webp，验证、预览、切换一个自定义槽。

**使用：** 兼容宿主上显示宠物后可抚摸、喂食，或分别导入 pet.json 和 spritesheet.webp。当前模板默认禁用。

**当前模板禁用此项。** 先确认目标宿主支持所需 API，再单独启用与验证。

[详细安装、配置、作者与限制](catalog/neystan--dsh-pet/README.zh-CN.md)。

### 皮肤合集 — `@neystan/dsh-skins`

- 聚合皮肤：内置十种皮肤资产与一个独立自定义主题槽。
- 互斥切换：dsh-skin use 管理激活，避免多个皮肤叠加。
- 外观控制：强调色、背景、前景、对比度与可复用 WebP 背景。

**使用：** 通过皮肤中心或 dsh-skin use 切换主题；同一时间只启用一个皮肤，避免外观叠加。

[详细安装、配置、作者与限制](catalog/neystan--dsh-skins/README.zh-CN.md)。

### 图像描述工具 — `@neystan/dsh-tool-describe-image`

- 图像输入：本地绝对路径、HTTP(S) URL 或附件引用，一次一张。
- 模型工具：describe_image 接受指定 OCR、图表、翻译等 prompt，只把返回文字写入会话。
- 协议：OpenAI 兼容 Chat Completions 或 Responses，设置修改即时生效。
- 边界：默认 10 MiB、1024 输出 tokens、60 秒；拒绝重定向并检查文件魔数。

**使用：** 兼容宿主上填写 baseURL 和视觉模型，再让 Agent 调用 describe_image 读取路径、URL 或附件。当前模板默认禁用。

**常用设置：** `baseURL / model` = `required`; `apiStyle` = `chat-completions`; `apiKeyEnv` = `VISION_API_KEY`; `maxBytes` = `10485760`; `maxOutputTokens` = `1024`; `timeoutMs` = `60000`

**当前模板禁用此项。** 先确认目标宿主支持所需 API，再单独启用与验证。

[详细安装、配置、作者与限制](catalog/neystan--dsh-tool-describe-image/README.zh-CN.md)。

### 皮肤中心 — `@neystan/dsh-client-ui-skin-center`

- 浏览与试穿：默认主题、内置皮肤、自定义主题，即时试穿和退出恢复。
- 应用：宿主写入 managed patch，配置 watcher 热加载并刷新页面。
- 自定义与背景：三色加对比度，Follow skin/Custom/None 背景模式；图片压缩为 WebP。

**使用：** 兼容宿主上打开插件配置中的皮肤中心，试穿后再应用，可调整颜色、对比度和背景。当前模板默认禁用。

**当前模板禁用此项。** 先确认目标宿主支持所需 API，再单独启用与验证。

[详细安装、配置、作者与限制](catalog/neystan--dsh-client-ui-skin-center/README.zh-CN.md)。

## 配置、隐私与使用边界

- 账号、API Key、机器人 Token、浏览器 Cookie、手机配对和隧道凭据在各自机器配置，不进入仓库。
- 图像理解可能把图片发送到配置的视觉服务；提示词优化可能把草稿发送到选择的模型；搜索请求会发送到对应搜索服务。
- 浏览器、Git 分支管理、手机访问和重启操作会影响真实环境，使用前确认目标与操作内容。
- 本地插件使用指向仓库的 `file:` 依赖；移动仓库后应从新路径重新生成 Profile。
- 根包版本与下载哈希记录在 [catalog.lock.json](catalog.lock.json)，传递依赖由新 Profile 生成的包管理器 lockfile 记录。

## 卸载与换机恢复

卸载某个插件：

```sh
dsh plugin --profile YOUR_PROFILE remove dsh-prompt-enhancer
```

换机时重新克隆仓库，安装 DSH 和依赖工具，再对一个新 Profile 执行 `--all --apply --fetch`，最后重新配置账号和外部服务。这恢复插件集合，不恢复聊天、个人设置、登录状态或私钥。合集安装器没有改动原来的 Profile，回退时可继续使用原 Profile。

## 作者与许可证

第三方插件属于各自原作者。本合集提供整理、文档与安装工具，不把下载的插件重新标为自创。原项目、fork 维护者、版本和许可证见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) 和各插件详情页。

- Web UI 原项目：zhu1090093659；当前 fork 维护者：neystan。
- purge 原项目：小杨 / YuJunZhiXue；社区版维护者：kingcharleslzy-ai。
- AionUI 面板的包声明与 LICENSE 文本不一致，已记录，未转载其运行源码。
- Liang 皮肤与本地 balance 未声明许可证；本地 restart 声明 MIT 但缺少原始版权声明，不虚构补全。

## 验证状态与常见问题

本地 10 项 Python 和 9 项 Node 测试通过；12 个顶层插件隔离安装成功，Linux/macOS CI 已通过。检查覆盖安装器、扫描器、余额核心和宿主路由等，**不代表所有在线服务、手机或浏览器界面已验证**。详见 [验证报告](docs/VERIFICATION.md) 和 [Actions](https://github.com/johnnyliu1126/deepseek-harness-plugin-collection/actions)。

| 问题 | 处理方式 |
|---|---|
| 找不到 `dsh` 命令 | 先确认宿主 CLI；macOS 内置路径见安装指南。 |
| 提示目标目录已存在 | 选择新的 Profile 名称；安装器不会覆盖已有目录。 |
| 安装后 Desktop 没有变化 | 新 Profile 不会自动切换 Desktop；如需现有 Profile 使用，应备份后按单插件流程添加。 |
| 看板、宠物或皮肤中心不显示 | 检查兼容性禁用项，先升级与复测宿主 API。 |
| 余额不显示或查询失败 | 先打开会话并确认宿主 DeepSeek 账号登录、account 服务可用。 |
| pnpm 提示构建授权 | 逐项检查上游构建要求；合集默认 `--ignore-scripts`，不要全局关闭保护。 |
| 手机插件提示 React peer 不匹配 | 参考对应版本上游兼容要求，不强行替换宿主 React 来掩盖问题。 |

## 仓库目录与维护

```text
catalog/                Plugin features, setup and provenance in both languages
plugins/                Local restart and balance-monitor source
licenses/               Observed upstream license texts
scripts/                Installer, metadata inventory and validation
templates/              Compatibility guards
docs/                   Installation, integrations, architecture and verification
tests/                  Installer/download/scanner and host-route checks
```

```sh
python3 scripts/check.py
python3 -m unittest discover -s tests -v
node --test plugins/dsh-balance-monitor/core.test.js tests/routes.test.mjs
```

额外 Playwright、Context7、GitHub、REA MCP 与六个独立本地 skill 的用途和排除范围见 [集成说明](docs/INTEGRATIONS.md)。
