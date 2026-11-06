# DeepSeek Harness Additional Plugin Collection

[English](README.md) | [简体中文](README.zh-CN.md) | [Downloads / 下载](https://github.com/johnnyliu1126/deepseek-harness-plugin-collection/releases/tag/v0.1.0)

A catalog of additional DeepSeek Harness plugins for discovering features, installing a subset and rebuilding a plugin environment on another machine.

The collection documents **19 plugin entries, 12 top-level install choices and 72 feature descriptions**. Two local plugins include source. Built-in DSH plugins are excluded; third-party packages retain their original authors/upstream links and are downloaded from pinned, integrity-checked distributions.

## Choose your platform

| Platform / 平台 | Repository / 仓库 |
|---|---|
| Mac Intel / x64 | [deepseek-harness-plugins-macos-intel](https://github.com/johnnyliu1126/deepseek-harness-plugins-macos-intel) |
| Mac M 系列 / arm64 | [deepseek-harness-plugins-macos-apple-silicon](https://github.com/johnnyliu1126/deepseek-harness-plugins-macos-apple-silicon) |
| Windows / x64 | [deepseek-harness-plugins-windows](https://github.com/johnnyliu1126/deepseek-harness-plugins-windows) |

Each edition has native architecture checks and its own CI. / 每版有独立架构检查与对应平台 CI。Windows 版排除 macOS 重启插件。

## Where to start

- Browse the tables below to see the installed additions.
- Read “Plugin features and usage” or follow a plugin link for detailed instructions.
- Use “Installation and launch” to install the full set or a subset.
- Download the source ZIP, two local plugin TGZs and SHA256SUMS from the [v0.1.0 prerelease](https://github.com/johnnyliu1126/deepseek-harness-plugin-collection/releases/tag/v0.1.0).

**Compatibility:** the template disables task board, pet, image description and skin center. Mobile has a React peer mismatch. Installation/declaration does not establish runtime compatibility; see verification below.

## Included plugins

### 12 top-level install choices

| Plugin | Version | Purpose | First use |
|---|---|---|---|
| [dsh-purge-community](catalog/dsh-purge-community/README.md) | 1.6.60 | Diagnostics, rules and patch management | Open the plugin sidebar, inspect diagnostics/backups, then manage preset prompts/rules or revert changes. |
| [@neystan/dsh-web-ui-all](catalog/neystan--dsh-web-ui-all/README.md) | 0.1.16 | Web UI aggregate | Install the aggregate and use its board, Git graph and file-panel entries; four compatibility-limited children remain disabled. |
| [dsh-lark-channel](catalog/dsh-lark-channel/README.md) | 0.0.7 | Feishu / Lark bot | Provision a Feishu/Lark bot with local credentials, then send it tasks; use /status, /ws, /cd, /model and /sessions. |
| [@tt-a1i/archify-dsh](catalog/tt-a1i--archify-dsh/README.md) | 1.0.0 | Architecture diagrams | Ask: “Use the archify skill to analyze this repository, generate architecture JSON and HTML, and return their file paths.” |
| [dsh-prompt-enhancer](catalog/dsh-prompt-enhancer/README.md) | 1.2.2 | Prompt optimization | Write a draft, click Optimize, review it, then send; settings offer concise, balanced, detailed and custom modes. |
| [@liustack/modlens](catalog/liustack--modlens/README.md) | 3.27.2 | Vision and OCR | Configure a vision provider, then ask: “Read this image, transcribe all text and explain the chart.” Diagnose with modlens doctor. |
| [@liustack/modsearch](catalog/liustack--modsearch/README.md) | 5.10.11 | Web and X search | Ask for search/fetch, e.g. “Search this technical question and include source links.” X search additionally needs configured Grok Build. |
| [dsh-ego-browser](catalog/dsh-ego-browser/README.md) | 0.9.8 | Browser automation | Ask the agent to navigate/interact and watch the side panel; use the plugin login-import flow or sign in manually when needed. |
| [dsh-client-liang-intensity-skin](catalog/dsh-client-liang-intensity-skin/README.md) | 0.1.6 | Reasoning slider and skin | Enable the skin, select a model with multiple reasoning efforts, then drag and release the slider to commit a level. |
| [dsh-restart](catalog/dsh-restart/README.md) | 1.0.0 | One-click restart | Click Restart in the macOS Desktop sidebar footer; finish active work first because a real restart interrupts tasks. |
| [dsh-balance-monitor](catalog/dsh-balance-monitor/README.md) | 1.0.0 | Balance monitor | Sign in through the host DeepSeek account UI and open a session; view the balance below the composer and click it for polling/threshold settings. |
| [dsh-mobile](catalog/dsh-mobile/README.md) | 0.8.2 | Mobile access | Choose LAN or a remote transport in mobile-access settings and pair by QR; configure accounts, tunnels and notifications locally. |

### 7 children of the Web UI aggregate

`@neystan/dsh-web-ui-all` pulls in these packages. Install a child directly when you need only a subset. **Do not select an aggregate and its child together.**

| Child | Purpose | Template status |
|---|---|---|
| [@neystan/dsh-client-ui-task-board](catalog/neystan--dsh-client-ui-task-board/README.md) | Task board, cron and todos | Disabled; upgrade/retest the host |
| [@neystan/dsh-client-ui-aionui-panel](catalog/neystan--dsh-client-ui-aionui-panel/README.md) | File tree and multi-tab preview | Not explicitly disabled; runtime compatibility still needs validation |
| [@neystan/dsh-client-ui-git-graph](catalog/neystan--dsh-client-ui-git-graph/README.md) | Git graph and branches | Not explicitly disabled; runtime compatibility still needs validation |
| [@neystan/dsh-pet](catalog/neystan--dsh-pet/README.md) | Companion interactions | Disabled; upgrade/retest the host |
| [@neystan/dsh-skins](catalog/neystan--dsh-skins/README.md) | Skin collection | Not explicitly disabled; runtime compatibility still needs validation |
| [@neystan/dsh-tool-describe-image](catalog/neystan--dsh-tool-describe-image/README.md) | Image-description tool | Disabled; upgrade/retest the host |
| [@neystan/dsh-client-ui-skin-center](catalog/neystan--dsh-client-ui-skin-center/README.md) | Skin center | Disabled; upgrade/retest the host |

## Installation and launch

### 1. Prerequisites

Install DeepSeek Harness separately, plus Python 3.10+, Node.js 22.19+ (24 recommended) and pnpm. The catalog snapshot observed host components at `0.2.1-rc.4`; check each plugin before using a different host version.

### 2. Clone

```sh
git clone https://github.com/johnnyliu1126/deepseek-harness-plugin-collection.git
cd deepseek-harness-plugin-collection
```

### 3. Preview, then install

`collection` is a new profile. The installer refuses an existing target and does not overwrite the active `desktop` profile.

```sh
# Preview only / 只读预览
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --all

# Create profile, verify downloads and install / 创建、校验并安装
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --all --apply --fetch
```

For a subset, replace `--all` with `--plugins`. This example creates another fresh profile with the two local plugins:

```sh
python3 scripts/collection.py \
  --target "$HOME/.dsh/profiles/collection-local" \
  --plugins dsh-restart dsh-balance-monitor \
  --apply --fetch
```

Flags: `--all` selects 12 roots; `--plugins` selects package names; `--apply` creates the profile; `--fetch` downloads/installs dependencies. Without `--apply`, the command only prints a plan. Dependency lifecycle scripts are disabled. The installer does not restart the app, sign in or expose a tunnel.

### 4. Inspect and launch the new profile

With a DSH CLI installed:

```sh
dsh --profile collection --dump-config
dsh --profile collection --help
dsh --profile collection
```

Creating `collection` does not change Desktop’s active profile. Check port options in `--help` before starting another web instance. If macOS Desktop has no CLI on PATH, see the [installation guide](docs/INSTALL.md) for the observed bundled CLI path.

### 5. Add one plugin to an existing profile

Back up that profile first, then use the host plugin manager. For example, add prompt optimization to `desktop`:

```sh
dsh plugin --profile desktop add dsh-prompt-enhancer@1.2.2
```

For a local plugin, use `dsh plugin --profile desktop add link:/absolute/repository/path/plugins/dsh-balance-monitor`. Let the plugin manager register dependencies/bundles; do not replace the existing package.json wholesale. Follow the plugin/host instructions for any required restart.

## Plugin features and usage

The following 72 feature descriptions are grounded in pinned source, manifests or packaged documentation. They describe the implementation and entry points, not a guarantee that every external service/UI flow has been exercised end to end.

### Diagnostics, rules and patch management — `dsh-purge-community`

- Status diagnostics: inspect patch and host evidence; a read failure is not an absent installation.
- Prompt and rule management: per-preset text, ordering, exclusions, and one-shot injection controls.
- Patch lifecycle: local backups, apply/revert and version management; host modification requires an explicit separate action.
- Lab workbench: packaged presets, skills, SQLite evidence store and /redteam/api bridge.
- Retry/continue: configurable retry limits and continuation text; success is not guaranteed.

**Use:** Open the plugin sidebar, inspect diagnostics/backups, then manage preset prompts/rules or revert changes.

**Common settings:** `autoApplyOnStart / autoUpdateOnStart` = `false`; `autoRetry / retryMax` = `true / 3`; `autoContinue / continueMax` = `false / 3`; `postPrompt` = `empty`

[Detailed setup, configuration, attribution and limits](catalog/dsh-purge-community/README.md).

### Web UI aggregate — `@neystan/dsh-web-ui-all`

- Aggregate installation: task board, Git graph, side panel, pet, image description and skins.
- Composition: a bundle patch mounts child plugins; install individual packages for a subset.
- Compatibility: some settings require newer keyed slots; four child rows are disabled in the observed profile.

**Use:** Install the aggregate and use its board, Git graph and file-panel entries; four compatibility-limited children remain disabled.

[Detailed setup, configuration, attribution and limits](catalog/neystan--dsh-web-ui-all/README.md).

### Feishu / Lark bot — `dsh-lark-channel`

- Chat-driven agents: Feishu/Lark messages launch host tasks with separate reasoning/tool/result views.
- Durable sessions: chat/thread/sender scopes, /new reset and /sessions continuation.
- Workspace/model controls: /ws, /cd, /model, /status and /stop.
- Interactive cards: questions, plan reviews and tool approvals subject to configured approvers.
- Multiple bots: separate credentials/sessions, botPeers allowlists and botHops loop bounds.
- File transfer: workspace inbox and per-send group approval, with a default 20 MiB per-file limit.

**Use:** Provision a Feishu/Lark bot with local credentials, then send it tasks; use /status, /ws, /cd, /model and /sessions.

**Common settings:** `sessionScope` = `see upstream schema`; `botHops` = `6`; `attachImages` = `false`; `receiveFiles / sendFiles` = `true`; `maxReceiveFileBytes / maxSendFileBytes` = `20 MiB`

[Detailed setup, configuration, attribution and limits](catalog/dsh-lark-channel/README.md).

### Architecture diagrams — `@tt-a1i/archify-dsh`

- Architecture skill: exposes Archify via a filesystem skill provider; invoke it by name.
- Structured artifacts: specification JSON and HTML diagrams with components, a main path and trust boundaries.
- Lightweight adapter: no extra native tools or Web UI; bundles Archify 3.0.1 independently of adapter version.

**Use:** Ask: “Use the archify skill to analyze this repository, generate architecture JSON and HTML, and return their file paths.”

**Common settings:** `archify-plugin` = `packaged skills root`

[Detailed setup, configuration, attribution and limits](catalog/tt-a1i--archify-dsh/README.md).

### Prompt optimization — `dsh-prompt-enhancer`

- Draft optimization: a composer button rewrites the draft before sending, with edit/undo opportunities.
- Instruction modes: concise, balanced (default), detailed and custom, with a short-chat over-expansion retry.
- Model routing: shared free channel, current model or fixed model; fallback may consume paid conversation quota.
- Diagnostics: settings test the channel and show the last actual route; settings are stored locally.

**Use:** Write a draft, click Optimize, review it, then send; settings offer concise, balanced, detailed and custom modes.

**Common settings:** `mode` = `balanced`; `DSH_FREE_CHANNEL_BASE_URL` = `upstream default`; `DSH_FREE_CHANNEL_API_KEY` = `unset`; `DSH_FREE_CHANNEL_MODEL` = `upstream default`

If the shared free channel fails, fallback may consume the current conversation model’s quota; optimization is not guaranteed to be free in every mode.

[Detailed setup, configuration, attribution and limits](catalog/dsh-prompt-enhancer/README.md).

### Vision and OCR — `@liustack/modlens`

- Image understanding: OCR, reading order, regions, entities and relationships for text-only models.
- Providers: Gemini, OpenAI-compatible, Anthropic, Antigravity, Claude and Kimi CLI backends.
- Failover/key rotation: authorization, rate-limit and quota failures can rotate keys or switch providers.
- CLI reuse: doctor discovers installed tools; explicitly configured reuse may consume their subscription quota.

**Use:** Configure a vision provider, then ask: “Read this image, transcribe all text and explain the chart.” Diagnose with modlens doctor.

[Detailed setup, configuration, attribution and limits](catalog/liustack--modlens/README.md).

### Web and X search — `@liustack/modsearch`

- Web search/fetch: search and page text for models without native web access.
- Engines: Firecrawl, Keenable, You.com, Antigravity, Tavily, Exa and local fetch.
- X search: available through a configured, authenticated Grok Build installation.
- Fallback/key rotation: switch failed channels; advertised free quotas are upstream claims and may change.

**Use:** Ask for search/fetch, e.g. “Search this technical question and include source links.” X search additionally needs configured Grok Build.

[Detailed setup, configuration, attribution and limits](catalog/liustack--modsearch/README.md).

### Browser automation — `dsh-ego-browser`

- Browser tools: ego_* tools drive the bundled ego-lite runtime for navigation and interaction.
- Live panel: SSE screencast, direct mouse control, tabs, download capture and human-verification notices.
- Login import: Chrome/Edge bridge or non-destructive profile copies; login data is excluded here.
- Host variants: Web side panel, optional TUI text UI and tools-only headless use.

**Use:** Ask the agent to navigate/interact and watch the side panel; use the plugin login-import flow or sign in manually when needed.

**Common settings:** `chromePath` = `auto-detect`; `defaultSpace` = `empty`

[Tool-by-tool reference for 35 browser tools](docs/BROWSER-TOOLS.md).

[Detailed setup, configuration, attribution and limits](catalog/dsh-ego-browser/README.md).

### Reasoning slider and skin — `dsh-client-liang-intensity-skin`

- Reasoning slider: maps the model’s actual reasoning.efforts evenly to 0–30.
- Commit behavior: drag previews; release, keyboard completion or blur snaps and commits the original effort ID.
- Visibility: hidden for unsupported/single-effort models and addressed subagents.
- Appearance: themed mode adds characters/background/colors; native mode restores the host UI.

**Use:** Enable the skin, select a model with multiple reasoning efforts, then drag and release the slider to commit a level.

**Common settings:** `appearance` = `user-selected`

[Detailed setup, configuration, attribution and limits](catalog/dsh-client-liang-intensity-skin/README.md).

### One-click restart — `dsh-restart`

- Persistent entry: sidebar footer button with an icon in collapsed mode.
- Restart flow: POST route launches a detached shell that terminates and relaunches the application.
- Diagnostics: state/log routes, dryRun preview and a 10-second duplicate-request debounce.
- Reconnect: browser polling reloads after host recovery; a real restart interrupts active tasks.

**Use:** Click Restart in the macOS Desktop sidebar footer; finish active work first because a real restart interrupts tasks.

**Common settings:** `DSH_RESTART_APP_PATH` = `/Applications/DeepSeek Harness.app`; `DSH_RESTART_DELAY_MS` = `700`; `DSH_RESTART_DRY_RUN` = `0`; `debounce` = `10000 ms`

[Detailed setup, configuration, attribution and limits](catalog/dsh-restart/README.md).

### Balance monitor — `dsh-balance-monitor`

- Balances: query host deepseekAccount; show recharge, bonus and total per currency.
- Refresh: 60-second default, 30/60/120/300 options, manual refresh, request merging and a 3-second throttle.
- Alert: default threshold 10 highlights low balances; settings persist in localStorage.
- Timing: Beijing-time workday windows/countdown with hardcoded 2026 holidays; not an official live pricing feed.
- Failure states: signed out, unsupported and failed are distinct; failures do not display zero balances.

**Use:** Sign in through the host DeepSeek account UI and open a session; view the balance below the composer and click it for polling/threshold settings.

**Common settings:** `刷新间隔 / interval` = `60 s`; `低余额阈值 / threshold` = `10`

Host account service only; no API-key queries, spending history or session estimates. Timing and the 2026 calendar are local algorithms, not an official live pricing feed.

[Detailed setup, configuration, attribution and limits](catalog/dsh-balance-monitor/README.md).

### Mobile access — `dsh-mobile`

- Mobile sessions: shared workspaces/messages/tools with touch-oriented composer, drawer and question cards.
- Clients: Android application and mobile browser/PWA, with customizable UI and device lists.
- Pairing: QR/link/key setup, multi-device reachability, switching, re-pairing and local-record removal.
- Networking: LAN, Tailscale, cpolar, Cloudflare, FRP, own proxy and Caddy; iroh is experimental and platform-limited.
- Notifications: iOS Home Screen Web Push and Android native alerts require explicit opt-in.
- Diagnostics/security: redacted connection reports, device credentials, Origin binding and per-path third-party WebSocket approvals.

**Use:** Choose LAN or a remote transport in mobile-access settings and pair by QR; configure accounts, tunnels and notifications locally.

**Common settings:** `pairing / network` = `configure in plugin UI`; `notifications` = `explicit opt-in`

Observed React warning: this package requests `^19.3.0`, while isolated installation resolved `18.3.1`. Successful installation does not certify mobile UI compatibility.

[Detailed setup, configuration, attribution and limits](catalog/dsh-mobile/README.md).

### Task board, cron and todos — `@neystan/dsh-client-ui-task-board`

- Task board: multi-column cards, host persistence and execution through real agent sessions.
- Scheduling: host cron with create/list/pause/resume/run/delete actions.
- Todos: add/list/complete/delete with durable storage.

**Use:** On a compatible host, open the board, add tasks/todos and configure cron for scheduled runs. Disabled by the current template.

**Disabled by the current template.** Confirm the target host supports its APIs before enabling/retesting it.

[Detailed setup, configuration, attribution and limits](catalog/neystan--dsh-client-ui-task-board/README.md).

### File tree and multi-tab preview — `@neystan/dsh-client-ui-aionui-panel`

- Explorer: workspace file tree, filename search and Git changes.
- Preview: multi-tab viewing for over ten formats using host fs/git services.

**Use:** Open the right panel to browse the workspace tree, search filenames, inspect Git changes and open preview tabs.

[Detailed setup, configuration, attribution and limits](catalog/neystan--dsh-client-ui-aionui-panel/README.md).

### Git graph and branches — `@neystan/dsh-client-ui-git-graph`

- Branches/graph: a branch selector and commit graph in the session header.
- Git operations: host-side branch creation/switching with guards.

**Use:** Use the session-header Git graph to inspect/select/create/switch repository branches; operations affect the real repository.

[Detailed setup, configuration, attribution and limits](catalog/neystan--dsh-client-ui-git-graph/README.md).

### Companion interactions — `@neystan/dsh-pet`

- Activity animation: nine states driven by session/tool events.
- Interaction: petting, feeding, affinity and treat stock persisted by the host.
- Customization: validate/preview/import pet.json and spritesheet.webp into one custom slot.

**Use:** On a compatible host, pet/feed the companion or import pet.json and spritesheet.webp separately. Disabled by the current template.

**Disabled by the current template.** Confirm the target host supports its APIs before enabling/retesting it.

[Detailed setup, configuration, attribution and limits](catalog/neystan--dsh-pet/README.md).

### Skin collection — `@neystan/dsh-skins`

- Skin collection: ten bundled skins and an independent custom-theme slot.
- Exclusive activation: dsh-skin use manages one active skin at a time.
- Appearance controls: accent/background/foreground/contrast and reusable WebP backgrounds.

**Use:** Switch themes through the skin center or dsh-skin use; keep one skin active to avoid overlapping styles.

[Detailed setup, configuration, attribution and limits](catalog/neystan--dsh-skins/README.md).

### Image-description tool — `@neystan/dsh-tool-describe-image`

- Inputs: one local absolute path, HTTP(S) URL or attachment reference per call.
- Tool: describe_image accepts OCR/chart/translation instructions and adds only returned text to the conversation.
- Protocols: OpenAI-compatible Chat Completions or Responses with live configuration.
- Bounds: defaults of 10 MiB, 1024 output tokens and 60 seconds; redirects refused and magic bytes checked.

**Use:** On a compatible host, configure baseURL/model and ask the agent to call describe_image on a path, URL or attachment. Disabled by the current template.

**Common settings:** `baseURL / model` = `required`; `apiStyle` = `chat-completions`; `apiKeyEnv` = `VISION_API_KEY`; `maxBytes` = `10485760`; `maxOutputTokens` = `1024`; `timeoutMs` = `60000`

**Disabled by the current template.** Confirm the target host supports its APIs before enabling/retesting it.

[Detailed setup, configuration, attribution and limits](catalog/neystan--dsh-tool-describe-image/README.md).

### Skin center — `@neystan/dsh-client-ui-skin-center`

- Browse/try-on: stock, bundled and custom themes with live preview and restoration on exit.
- Apply: host updates the managed patch; config watching reloads it and refreshes the page.
- Customization/backgrounds: three colors plus contrast; Follow skin/Custom/None modes and WebP normalization.

**Use:** On a compatible host, open Skin Center in plugin settings, try on/apply themes and adjust colors, contrast/backgrounds. Disabled by the current template.

**Disabled by the current template.** Confirm the target host supports its APIs before enabling/retesting it.

[Detailed setup, configuration, attribution and limits](catalog/neystan--dsh-client-ui-skin-center/README.md).

## Configuration, privacy and operational scope

- Configure accounts, API keys, bot tokens, browser cookies, mobile pairing and tunnel credentials locally; none are included in the repository.
- Vision may send images to the configured vision service; prompt optimization may send drafts to the selected model; queries go to the selected search engine.
- Browser actions, Git branch controls, mobile access and restart affect real environments. Check the target and action first.
- Local packages use `file:` references into the checkout. Regenerate the profile after relocating it.
- [catalog.lock.json](catalog.lock.json) records root versions/download integrity. The new profile’s package-manager lockfile records transitive dependencies.

## Uninstall and restore

Remove an individual plugin:

```sh
dsh plugin --profile YOUR_PROFILE remove dsh-prompt-enhancer
```

On another machine, clone again, install DSH/prerequisites and run `--all --apply --fetch` against a new profile. Reconfigure accounts/external services locally. This restores the plugin set, not chats, personal settings, sign-ins or private keys. The installer leaves the original profile unchanged, so rollback can return to it.

## Authors and licenses

Third-party plugins belong to their original authors. This repository supplies organization, documentation and installation tools without relabeling downloaded plugins as original work. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) and plugin pages for original projects, fork maintainers, versions/licenses.

- Web UI original author: zhu1090093659; fork maintainer: neystan.
- purge original author: 小杨 / YuJunZhiXue; community maintainer: kingcharleslzy-ai.
- AionUI panel metadata and LICENSE disagree; the discrepancy is documented and its runtime source is not vendored.
- Liang skin and local balance have no declared license. Local restart declares MIT without an original copyright notice; missing facts are not fabricated.

## Verification and troubleshooting

10 Python and 9 Node tests passed locally. All 12 roots installed in isolation, and Linux/macOS CI passed. Checks cover the installer/scanner, balance core and host-route contracts; **they do not establish that all online services/mobile/browser UIs work**. See the [verification report](docs/VERIFICATION.md) and [Actions](https://github.com/johnnyliu1126/deepseek-harness-plugin-collection/actions).

| Problem | What to check |
|---|---|
| `dsh` not found | Locate the host CLI; the observed macOS bundled path is in the installation guide. |
| Target directory exists | Choose a new profile name; existing directories are never overwritten. |
| Desktop looks unchanged | A new profile does not switch Desktop automatically; back up and add selected packages to its existing profile if desired. |
| Board/pet/skin center missing | Check compatibility disables and retest against a host with the required APIs. |
| Balance missing/failing | Open a session and check host account sign-in/account-service availability. |
| pnpm build approval warning | Review upstream build requirements individually; the collection defaults to `--ignore-scripts`. |
| Mobile React peer mismatch | Follow upstream version compatibility; do not force-replace host React to conceal it. |

## Layout and maintenance

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

For the additional Playwright, Context7, GitHub and REA MCP integrations and six loose local skills, see [integration notes](docs/INTEGRATIONS.md).
