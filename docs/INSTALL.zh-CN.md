# 安装与恢复

[English](INSTALL.md) | [简体中文](INSTALL.zh-CN.md)

单独安装 DSH 宿主。本仓库不包含官方 bundle 源码、SDK 二进制、模型权重或登录状态。盘点机器为 macOS x86_64，宿主组件 0.2.1-rc.4；这不是对所有版本的兼容保证。

## 创建独立 Profile

在仓库根目录操作。目标必须是不存在的新目录。`--all` 选择 12 个顶层额外插件，`--plugins 包名 [包名 ...]` 选择部分；Web UI 子包也能单独选，但不能与对应聚合包重复。

```sh
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --plugins dsh-restart dsh-balance-monitor
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --plugins dsh-restart dsh-balance-monitor --apply --fetch
```

第一条只输出计划。第二条在临时目录生成 Profile，按 catalog 的 SRI 校验上游根包，执行 `pnpm install --ignore-scripts`，成功后转入目标目录。可用 `--manager npm` 检查本地包；完整合集推荐 pnpm。生命周期脚本默认禁用，必要的上游构建步骤需单独审查。失败暂存目录会保留并在错误中显示。

仅 `--apply` 不加 `--fetch` 只生成配置。账号、隧道、机器人和浏览器登录仍需在本机配置。清单固定根插件版本；传递依赖由新 Profile 生成的包管理器 lockfile 记录，不声称 catalog 冻结所有传递依赖。保留该 lockfile，后续使用 `pnpm install --frozen-lockfile --ignore-scripts`。

本地源码通过 `file:` 指向仓库 `plugins/`，请保留 checkout 路径。移动仓库后从新位置创建新 Profile。安装回执不等于可跨机器直接复用的 lockfile。

## 显式启动

新 Profile 不会切换 Desktop 正在使用的 `desktop`。如果安装了 CLI，先检查：

```sh
dsh --profile collection --dump-config
dsh --profile collection --help
dsh --profile collection
```

本机 macOS Desktop 没有 `dsh` PATH 命令，可使用观察到的内置 CLI：

```sh
node "/Applications/DeepSeek Harness.app/Contents/Resources/app/dsh/node_modules/@deepseek-ai/dsh/lib/bin.js" --profile collection --dump-config
```

这条路径仅对应本机应用布局，其他版本用匹配宿主的 CLI。base/web 只是宿主依赖引用，官方源码未上传。启动新 Web 实例前从 `--help` 查看端口选项，选择空闲端口，并逐项确认权限与必要配置。安装器不会关闭或重启现有 Desktop。

如要把单项插件装进现有 Profile，先将该 Profile 备份到新的带时间戳本地目录，再执行对应文档中的 `dsh plugin --profile NAME add SPEC`。本地插件使用 `add link:/仓库绝对路径/plugins/dsh-restart` 或 balance-monitor。由插件管理器更新依赖与 bundle，不要整份覆盖现有 package.json。合集安装器为避免破坏现有设置，拒绝合并已有目录。

## 恢复与回退

换电脑后克隆仓库，在新 Profile 路径执行 `--all --apply --fetch`，重新登录账号、配置机器人/视觉服务、手机配对。安装器不导出这些凭据。恢复的是额外插件集合与兼容性保护，不是个人设置和聊天的逐字节备份。

回退时使用原来的 Profile，它没有被安装器修改。如果手工安装到了现有 Profile，可在 DSH 停止时恢复自己的本地备份，或执行 `dsh plugin --profile NAME remove PACKAGE` 只移除新增包。不要删除整个 `~/.dsh`、会话或凭据库。卸载插件不会自动清除它的私人运行状态。

## 已知限制

- 四个 Web UI 子项保持禁用，见 compatibility.patch；升级宿主并复测后再启用。
- 安装器拒绝聚合包/子包重复选择；同时只启用一种皮肤。
- restart 只能真正重启 macOS Desktop 的 .app 宿主，普通 Node Web 进程不会变成 Desktop。
- balance 使用宿主账号；2026 节假日算法不是当前官方计费证明。
- purge 从固定 GitHub Release 下载并校验哈希；修改宿主需单独显式操作，安装器不触发。
- 免费通道、远程传输、手机通知、浏览器登录导入依赖外部服务和平台，未逐一在线验证。
