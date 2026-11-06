# Installation and restoration

[English](INSTALL.md) | [简体中文](INSTALL.zh-CN.md)

Install DSH separately. The repository contains no official DSH bundle source, SDK binaries, model weights or authentication state. The observed host components were 0.2.1-rc.4 on macOS x86_64; this is a snapshot rather than a promise of support on every release.

## Create a separate profile

Run commands from the repository root. `--target` must be a new directory. Use `--all` for the 12 top-level additions or `--plugins NAME [NAME ...]` for a subset. Nested Web UI packages can be selected individually, but not together with their aggregate.

```sh
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --plugins dsh-restart dsh-balance-monitor
python3 scripts/collection.py --target "$HOME/.dsh/profiles/collection" --plugins dsh-restart dsh-balance-monitor --apply --fetch
```

The first command prints a plan. The second stages a new profile, verifies downloaded root tarballs against the catalog SRI hashes, runs `pnpm install --ignore-scripts`, then moves the completed profile into place. `--manager npm` is available for local-package checks; pnpm is recommended for the full collection. Dependency lifecycle scripts remain disabled; review any necessary upstream build steps separately. A failed staging directory is retained for inspection, and the error identifies it.

`--apply` without `--fetch` creates only configuration. Credentials, remote tunnels, bot setup and browser sign-ins are separate local steps. The manifest pins root plugin versions; transitive dependency resolution is recorded by the target profile's generated package-manager lockfile, rather than claiming the catalog freezes every transitive version. Preserve that lockfile for a subsequent `pnpm install --frozen-lockfile --ignore-scripts`.

The source checkout must stay at its current path: local plugins use `file:` dependencies pointing into `plugins/`. After moving the checkout, generate a new profile from the new location. Do not copy a receipt to a different computer as an installable lockfile.

## Launch explicitly

A new profile does not change the Desktop app's active `desktop` profile. If a DSH CLI is installed, inspect configuration before starting:

```sh
dsh --profile collection --dump-config
dsh --profile collection --help
dsh --profile collection
```

If macOS Desktop has no `dsh` command on PATH, its observed bundled CLI can be used without installing a second host:

```sh
node "/Applications/DeepSeek Harness.app/Contents/Resources/app/dsh/node_modules/@deepseek-ai/dsh/lib/bin.js" --profile collection --dump-config
```

This path is specific to the observed app layout. Use the matching host's CLI; do not treat it as universal. The profile includes references to built-in base/web bundles, resolved by that host; no official source is copied here. Choose an unused port in the app's `--help` before launching another web surface. Review each plugin's permissions and required settings before enabling it. The collection does not stop or restart the active Desktop app.

To install a single addition into an already configured profile instead, first back up that profile to a new timestamped local directory, then use the plugin's documented `dsh plugin --profile NAME add SPEC` command. The collection installer intentionally refuses to merge into an existing profile. For a local plugin use `add link:/absolute/path/to/this/repository/plugins/dsh-restart` (or balance monitor). DSH plugin manager handles dependency/bundle registration; never replace an entire existing package.json with the collection template.

## Restore and rollback

On a new machine, clone the repository and repeat `--all --apply --fetch` into a new profile. Reconfigure account sign-in, bot credentials, vision providers and mobile pairing locally. The installer never exports these values. This restores the addition set and compatibility guards, not a byte-for-byte copy of personal settings or chats.

For rollback, return to your previously active profile: the installer has not modified it. For manual installation into an existing profile, restore your local backup while DSH is stopped or remove only the package you added using `dsh plugin --profile NAME remove PACKAGE`. Do not delete global `~/.dsh`, sessions or credential stores. Uninstalling a plugin does not automatically erase its private runtime state.

## Known constraints

- Four Web UI children remain disabled by `templates/compatibility.patch.yml` until host API compatibility is retested.
- Aggregate/child duplication is rejected by the installer. Only one skin should be active.
- `dsh-restart` actually restarts only a macOS Desktop `.app` host. Starting a normal Node web profile does not make it a Desktop process.
- Balance monitor uses the host account service; the 2026 holiday/time algorithm is a local implementation, not verified current billing advice.
- Purge comes from a fixed GitHub release URL, not a missing npm version. Its hash is pinned. Host patching is a separate explicit operation, never a side effect of this collection's installer.
- Free endpoints, remote transports, mobile notification delivery and browser import depend on external services/platforms and were not exhaustively tested here.
