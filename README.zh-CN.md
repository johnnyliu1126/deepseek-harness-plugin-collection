# DeepSeek Harness Plugin Collection

[English](README.md) | [简体中文](README.zh-CN.md)

我的额外插件合集：19 个插件条目、12 个顶层安装项、2 个本地源码包。每个功能都有中英文说明、来源和验证边界。

**不上传 DeepSeek Harness 自带插件。** 第三方运行源码也不整包复制：锁定上游版本与分发哈希，通过安装器拉取；本地维护的 restart、balance 附带源码。

## 快速开始

需要 Python 3.10+、Node 22.19+（推荐 24）和 pnpm；DSH 宿主单独安装。本次盘点的宿主组件版本是 0.2.1-rc.4。

```sh
git clone https://github.com/johnnyliu1126/deepseek-harness-plugin-collection.git
cd deepseek-harness-plugin-collection
# Read-only plan / 只读预览
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --all
# Create a fresh profile and fetch verified upstream roots / 新建并安装
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --all --apply --fetch
```

选择单项时把 `--all` 换成 `--plugins dsh-balance-monitor` 等包名。已有目标目录会被拒绝；不覆盖 desktop、不导出凭据、不重启正在运行的应用。四个已知不兼容子项默认保持禁用。

完整安装、恢复、启动、回滚和限制见 [中文指南](docs/INSTALL.zh-CN.md)。

## 插件目录

| Plugin | Version | Features / 功能 | Origin / 来源 |
|---|---|---|---|
| [dsh-purge-community](catalog/dsh-purge-community/README.zh-CN.md) | 1.6.60 | 状态自检与宿主证据：面板检查补丁和运行状态，失败读取不等于未安装。 | 上游安装 / upstream install |
| [@neystan/dsh-web-ui-all](catalog/neystan--dsh-web-ui-all/README.zh-CN.md) | 0.1.16 | 聚合安装：一次安装任务看板、Git 图、右侧面板、宠物、图像描述和皮肤包。 | 上游安装 / upstream install |
| [dsh-lark-channel](catalog/dsh-lark-channel/README.zh-CN.md) | 0.0.7 | 聊天驱动 Agent：飞书/Lark 文本触发真实宿主任务，推理、工具和结果分开展示。 | 上游安装 / upstream install |
| [@tt-a1i/archify-dsh](catalog/tt-a1i--archify-dsh/README.zh-CN.md) | 1.0.0 | 架构图技能：通过文件系统 skill provider 提供 Archify，按名称调用。 | 上游安装 / upstream install |
| [dsh-prompt-enhancer](catalog/dsh-prompt-enhancer/README.zh-CN.md) | 1.2.2 | 草稿优化：输入框按钮替换草稿，保留发送前编辑和撤销的机会。 | 上游安装 / upstream install |
| [@liustack/modlens](catalog/liustack--modlens/README.zh-CN.md) | 3.27.2 | 图像理解：为文本模型补充 OCR、阅读顺序、区域、实体和关系描述。 | 上游安装 / upstream install |
| [@liustack/modsearch](catalog/liustack--modsearch/README.zh-CN.md) | 5.10.11 | 网页搜索与抓取：给没有原生联网能力的模型提供搜索与页面正文。 | 上游安装 / upstream install |
| [dsh-ego-browser](catalog/dsh-ego-browser/README.zh-CN.md) | 0.9.8 | 浏览器工具：ego_* 工具驱动内置 ego-lite，执行页面访问和交互。 | 上游安装 / upstream install |
| [dsh-client-liang-intensity-skin](catalog/dsh-client-liang-intensity-skin/README.zh-CN.md) | 0.1.6 | 推理滑块：读取模型实际 reasoning.efforts，均匀映射到 0–30。 | 上游安装 / upstream install |
| [dsh-restart](catalog/dsh-restart/README.zh-CN.md) | 1.0.0 | 常驻入口：侧边栏页脚文字按钮，窄栏降级为图标。 | 本地源码 / local source |
| [dsh-balance-monitor](catalog/dsh-balance-monitor/README.zh-CN.md) | 1.0.0 | 余额：通过宿主 deepseekAccount 查询，按币种展示充值、赠金和合计。 | 本地源码 / local source |
| [dsh-mobile](catalog/dsh-mobile/README.zh-CN.md) | 0.8.2 | 手机会话：与桌面共享 Workspace、消息和工具，适配触屏输入框、抽屉和问答卡片。 | 上游安装 / upstream install |
|  ↳[@neystan/dsh-client-ui-task-board](catalog/neystan--dsh-client-ui-task-board/README.zh-CN.md) | 0.1.16 | 任务看板：多列卡片、宿主持久化和真实 Agent 会话执行。 | 上游安装 / upstream install |
|  ↳[@neystan/dsh-client-ui-aionui-panel](catalog/neystan--dsh-client-ui-aionui-panel/README.zh-CN.md) | 0.1.16 | 文件管理：Workspace 文件树、文件名搜索与 Git 改动。 | 上游安装 / upstream install |
|  ↳[@neystan/dsh-client-ui-git-graph](catalog/neystan--dsh-client-ui-git-graph/README.zh-CN.md) | 0.1.16 | 分支与图：会话顶部的分支选择器和提交关系图。 | 上游安装 / upstream install |
|  ↳[@neystan/dsh-pet](catalog/neystan--dsh-pet/README.zh-CN.md) | 0.1.16 | 活动动画：会话与工具事件驱动九种动画状态。 | 上游安装 / upstream install |
|  ↳[@neystan/dsh-skins](catalog/neystan--dsh-skins/README.zh-CN.md) | 0.1.16 | 聚合皮肤：内置十种皮肤资产与一个独立自定义主题槽。 | 上游安装 / upstream install |
|  ↳[@neystan/dsh-tool-describe-image](catalog/neystan--dsh-tool-describe-image/README.zh-CN.md) | 0.1.16 | 图像输入：本地绝对路径、HTTP(S) URL 或附件引用，一次一张。 | 上游安装 / upstream install |
|  ↳[@neystan/dsh-client-ui-skin-center](catalog/neystan--dsh-client-ui-skin-center/README.zh-CN.md) | 0.1.16 | 浏览与试穿：默认主题、内置皮肤、自定义主题，即时试穿和退出恢复。 | 上游安装 / upstream install |

## 署名、权限与兼容性

所有下载插件保留原作者和维护者；原项目与 fork 都列出。参见 [署名清单](THIRD_PARTY_NOTICES.md) 与 [许可证说明](LICENSE)。未声明的许可证保持未声明，不将上游作品标为本仓库原创。

任务看板、宠物、图像描述、皮肤中心在盘点机器上被兼容性 patch 禁用。第三方在线服务与端到端 UI 并未全部测试；本地测试结果见 [验证报告](docs/VERIFICATION.md)。

## 维护

```sh
python3 scripts/check.py
python3 -m unittest discover -s tests -v
node --test plugins/dsh-balance-monitor/core.test.js tests/routes.test.mjs
python3 scripts/inventory.py --profile "$HOME/.dsh/profiles/desktop" --output additions.json
```

`inventory.py` 只提取包元信息，不读取账号、聊天或私人配置值。新增版本需重新审查功能和许可证后更新锁定清单。额外 MCP 与本地 skills 的边界见 [集成说明](docs/INTEGRATIONS.md)。

**Known install warning / 安装警告:** dsh-mobile requests React ^19.3.0 while the isolated graph resolved 18.3.1. See the verification report before enabling mobile access. / 手机插件存在 React peer 版本不匹配，启用前请看验证报告。
