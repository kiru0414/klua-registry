![logo](https://raw.githubusercontent.com/kiru0414/klua/refs/heads/main/docs/asset/logo-1.svg)

# klua official registry

This repository is the official alias registry (`kiru0414/klua-registry`) for [klua](https://github.com/kiru0414). By default, `klua` fetches alias shards at runtime from:

That URL is embedded as the default registry in `builtin/default_init.lua`.

## Shard format

Each `v1/<char>.yaml` file is a flat YAML mapping of `alias: scheme-target`. The shard character is the lowercase first letter of the alias (`a`–`z`); aliases starting with a digit or symbol live in `v1/_.yaml`.

## Supported target schemes

### [Documents](https://readthedocs.io)

### Example

* `gh:user/repo[@tag]` — GitHub Releases (or in-repo `klua.yaml` build)
* `gl:user/repo[@tag]` — GitLab Releases
* `url:https://...` — Direct archive or binary URL
* `sys:pkg1,pkg2` — System package manager delegation (`apt:`, `dnf:`, `pacman:`, `apk:`, `brew:` are also supported)
* `<alias>` — Recursive reference to another bare alias in the registry (e.g., `rg: ripgrep`)

## Contributions welcome!

We are actively expanding the registry and welcome pull requests adding popular CLI tools, developer utilities, and convenient command aliases!

## How to add aliases

1. Fork this repository (`kiru0414/klua-registry`).
2. Pick the shard file under `v1/` matching the alias's first character (`v1/a.yaml` through `v1/z.yaml`, or `v1/_.yaml` for digits/symbols).
3. Add your entry as `alias: scheme-target`, keeping entries sorted alphabetically.
4. Open a pull request. No rebuild of `klua` is needed — registries are fetched dynamically at runtime, so merged aliases become available immediately.

## Guidelines for new entries

* **Prefer upstream releases**: Point `gh:` / `gl:` targets at official upstream repositories that publish prebuilt release assets (or provide a `klua.yaml` manifest with `build.steps`).
* **Include command aliases**: If a tool's binary name differs from its project name, add the command name as a recursive alias pointing to the canonical entry (e.g., `ripgrep: gh:BurntSushi/ripgrep` and `rg: ripgrep`).
* **Use `sys:` for OS-level tools**: For tools without standalone GitHub/GitLab release binaries (or system libraries), use `sys:<package>` so `klua` can delegate cleanly to the host package manager.
* **Keep it sorted & duplicate-free**: Ensure keys are in alphabetical order and avoid duplicate entries within the same shard.
