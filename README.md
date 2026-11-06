# DeepSeek Harness Plugin Collection

[English](README.md) | [简体中文](README.zh-CN.md)

A collection of my additional plugins: 19 documented entries, 12 top-level install choices and 2 local source packages, with bilingual features, attribution and explicit validation limits.

**Built-in DeepSeek Harness plugins are not uploaded.** Third-party runtime source stays upstream: versions/distribution hashes are recorded for the installer. Locally maintained restart and balance packages include source.

## Quick start

Requires Python 3.10+, Node 22.19+ (24 recommended), pnpm and a separately installed DSH host. Observed host components: 0.2.1-rc.4.

```sh
git clone https://github.com/johnnyliu1126/deepseek-harness-plugin-collection.git
cd deepseek-harness-plugin-collection
# Read-only plan / 只读预览
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --all
# Create a fresh profile and fetch verified upstream roots / 新建并安装
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --all --apply --fetch
```

Replace `--all` with `--plugins dsh-balance-monitor` or other names to install a subset. Existing targets are refused. The installer does not overwrite desktop, export credentials or restart a live app. Four known incompatible child rows remain disabled by default.

For installation, restoration, launch, rollback and limitations, see the [English guide](docs/INSTALL.md).

## Plugin directory

| Plugin | Version | Features / 功能 | Origin / 来源 |
|---|---|---|---|
| [dsh-purge-community](catalog/dsh-purge-community/README.md) | 1.6.60 | Status diagnostics: inspect patch and host evidence; a read failure is not an absent installation. | 上游安装 / upstream install |
| [@neystan/dsh-web-ui-all](catalog/neystan--dsh-web-ui-all/README.md) | 0.1.16 | Aggregate installation: task board, Git graph, side panel, pet, image description and skins. | 上游安装 / upstream install |
| [dsh-lark-channel](catalog/dsh-lark-channel/README.md) | 0.0.7 | Chat-driven agents: Feishu/Lark messages launch host tasks with separate reasoning/tool/result views. | 上游安装 / upstream install |
| [@tt-a1i/archify-dsh](catalog/tt-a1i--archify-dsh/README.md) | 1.0.0 | Architecture skill: exposes Archify via a filesystem skill provider; invoke it by name. | 上游安装 / upstream install |
| [dsh-prompt-enhancer](catalog/dsh-prompt-enhancer/README.md) | 1.2.2 | Draft optimization: a composer button rewrites the draft before sending, with edit/undo opportunities. | 上游安装 / upstream install |
| [@liustack/modlens](catalog/liustack--modlens/README.md) | 3.27.2 | Image understanding: OCR, reading order, regions, entities and relationships for text-only models. | 上游安装 / upstream install |
| [@liustack/modsearch](catalog/liustack--modsearch/README.md) | 5.10.11 | Web search/fetch: search and page text for models without native web access. | 上游安装 / upstream install |
| [dsh-ego-browser](catalog/dsh-ego-browser/README.md) | 0.9.8 | Browser tools: ego_* tools drive the bundled ego-lite runtime for navigation and interaction. | 上游安装 / upstream install |
| [dsh-client-liang-intensity-skin](catalog/dsh-client-liang-intensity-skin/README.md) | 0.1.6 | Reasoning slider: maps the model’s actual reasoning.efforts evenly to 0–30. | 上游安装 / upstream install |
| [dsh-restart](catalog/dsh-restart/README.md) | 1.0.0 | Persistent entry: sidebar footer button with an icon in collapsed mode. | 本地源码 / local source |
| [dsh-balance-monitor](catalog/dsh-balance-monitor/README.md) | 1.0.0 | Balances: query host deepseekAccount; show recharge, bonus and total per currency. | 本地源码 / local source |
| [dsh-mobile](catalog/dsh-mobile/README.md) | 0.8.2 | Mobile sessions: shared workspaces/messages/tools with touch-oriented composer, drawer and question cards. | 上游安装 / upstream install |
|  ↳[@neystan/dsh-client-ui-task-board](catalog/neystan--dsh-client-ui-task-board/README.md) | 0.1.16 | Task board: multi-column cards, host persistence and execution through real agent sessions. | 上游安装 / upstream install |
|  ↳[@neystan/dsh-client-ui-aionui-panel](catalog/neystan--dsh-client-ui-aionui-panel/README.md) | 0.1.16 | Explorer: workspace file tree, filename search and Git changes. | 上游安装 / upstream install |
|  ↳[@neystan/dsh-client-ui-git-graph](catalog/neystan--dsh-client-ui-git-graph/README.md) | 0.1.16 | Branches/graph: a branch selector and commit graph in the session header. | 上游安装 / upstream install |
|  ↳[@neystan/dsh-pet](catalog/neystan--dsh-pet/README.md) | 0.1.16 | Activity animation: nine states driven by session/tool events. | 上游安装 / upstream install |
|  ↳[@neystan/dsh-skins](catalog/neystan--dsh-skins/README.md) | 0.1.16 | Skin collection: ten bundled skins and an independent custom-theme slot. | 上游安装 / upstream install |
|  ↳[@neystan/dsh-tool-describe-image](catalog/neystan--dsh-tool-describe-image/README.md) | 0.1.16 | Inputs: one local absolute path, HTTP(S) URL or attachment reference per call. | 上游安装 / upstream install |
|  ↳[@neystan/dsh-client-ui-skin-center](catalog/neystan--dsh-client-ui-skin-center/README.md) | 0.1.16 | Browse/try-on: stock, bundled and custom themes with live preview and restoration on exit. | 上游安装 / upstream install |

## Credits, permissions and compatibility

Downloaded plugins retain original authors and fork maintainers. See [credits](THIRD_PARTY_NOTICES.md) and [license scope](LICENSE). Missing licenses stay undeclared; upstream work is not relabeled as original to this collection.

Task board, pet, image description and skin center are disabled by the observed compatibility patch. External services and every UI flow were not all tested; see the [verification report](docs/VERIFICATION.md).

## Maintenance

```sh
python3 scripts/check.py
python3 -m unittest discover -s tests -v
node --test plugins/dsh-balance-monitor/core.test.js tests/routes.test.mjs
python3 scripts/inventory.py --profile "$HOME/.dsh/profiles/desktop" --output additions.json
```

`inventory.py` extracts package metadata without reading account data, chats or private configuration values. Review features/licenses before updating the catalog. See [integration notes](docs/INTEGRATIONS.md) for additional MCP servers and local skills.

**Known install warning / 安装警告:** dsh-mobile requests React ^19.3.0 while the isolated graph resolved 18.3.1. See the verification report before enabling mobile access. / 手机插件存在 React peer 版本不匹配，启用前请看验证报告。
