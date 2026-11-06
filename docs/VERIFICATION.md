# Verification report / 验证报告

Snapshot: 2026-11-06. Validation distinguishes installed/configured code from actual online use.
验证区分源码、安装与配置组合，不把安装成功写成所有在线功能均可用。

| Check / 检查 | Result / 结果 |
|---|---|
| Metadata-only inventory of extra plugins | 19 resolved, 0 unresolved; built-in packages excluded / 19 个额外包，0 未解析 |
| Python installer/inventory/scanner/download tests | 10 passed / 10 项通过 |
| Node balance-core and host-route tests | 9 passed / 9 项通过 |
| Local source installation | 2 packages installed with npm in a separate temporary Profile / 两个本地包隔离安装成功 |
| Full root set installation | 12 direct additions installed; verified upstream tarballs; pnpm installed 168 dependency packages with scripts disabled / 12 个根项安装成功，根包哈希校验通过，生命周期脚本禁用 |
| Host configuration composition | Local-only and full profiles composed with bundled DSH 0.2.1-rc.4 CLI `--dump-config`; no host mounting or live app restart / 两种组合配置均可生成，未挂载或重启现有宿主 |
| Root-package registry availability | 16 npm package/version records found; purge fetched from fixed GitHub v1.6.60 release / 16 个 npm 版本可解析，purge 使用固定 Release |
| Imported runtime source | Content hashes match the local originals; only packaging metadata/documentation changed / 运行源码哈希保持一致 |
| Archives | Local npm packages packed and inspected; final source archive excludes private state / 本地插件包与源码归档按白名单检查 |
| Catalog, paired docs, local links and secret heuristic | Run by `python3 scripts/check.py`; also enforced by CI / 本地检查与 CI 检查 |

## Warnings observed / 实测警告

- `pnpm peers check` reports `dsh-mobile@0.8.2` needs React `^19.3.0`, while the isolated dependency graph has `18.3.1`. Full install exits successfully; mobile UI compatibility is **not** certified. The host's React was not replaced.
- The purge bundle emits five “entry not found” warnings for retired standalone redteam rows while composing a fresh profile. These are upstream compatibility-disable rows; composition exits successfully. They were not silently removed from upstream code.
- Four Web UI rows remain disabled by the observed compatibility guards: task board, pet, describe-image and skin center. Only relevant guards are written for subset profiles.
- One first-attempt Archify download was truncated (200,522 bytes versus the subsequent full 1,774,405-byte response). Integrity validation refused installation. A fresh download passed its recorded SRI. The installer now checks declared Content-Length as well as SRI; it never accepts a mismatched archive.
- AionUI panel package metadata says Apache-2.0 while its installed LICENSE says BSD-3-Clause. No runtime code from it is redistributed; both facts are documented.
- The Liang skin and local balance monitor have no declared package license. The local restart package declares MIT but has no original copyright notice. Missing author/license facts are not invented.

上述警告均保留：手机 React peer 不匹配、purge 的旧条目兼容性提示、四项 UI 禁用、一次被校验拦截的不完整下载，以及许可证缺失或冲突。它们不等于全部插件已在真实 UI 验证。

## Not exercised / 未执行

No real application restart, balance request to a signed-in account, bot message, browser-cookie import, mobile pairing/tunnel exposure, notification delivery, third-party model request or full end-to-end UI compatibility run was performed for this release. Existing Desktop profile and credentials were not changed. External account setup must be completed locally by each user.
未实际重启应用、查询登录账号余额、发送机器人消息、导入浏览器 Cookie、手机配对/公开隧道、投递通知、调用第三方模型或完成全量 UI 端到端测试。现有 Desktop Profile 与凭据未修改。

## Reproduce / 复现

```sh
python3 scripts/check.py
python3 -m unittest discover -s tests -v
node --test plugins/dsh-balance-monitor/core.test.js tests/routes.test.mjs
python3 scripts/collection.py --target /absolute/new/test-profile --all --apply --fetch
```

GitHub Actions checks the source collection on Linux and macOS. A configured workflow is not itself proof of a successful remote run; inspect the actual Actions run status.
GitHub Actions 配置了 Linux/macOS 检查；工作流文件存在不代表远端已通过，应查看实际运行结果。
