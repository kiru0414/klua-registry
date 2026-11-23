# klua official registry template

This folder is the starter content for the official alias registry
(`kiru0414/klua-registry`). Push it to a public GitHub repository named
`klua-registry`; klua fetches shards from:

```
https://raw.githubusercontent.com/kiru0414/klua-registry/main/v1/<char>.yaml
```

That URL is the default registry embedded in `builtin/default_init.lua`.

## Shard format

Each `v1/<char>.yaml` file is a flat YAML mapping of alias -> scheme target.
The shard character is the lowercase first letter of the alias; aliases
starting with a non-letter live in `v1/_.yaml`.

```yaml
fd: gh:sharkdp/fd
fzf: gh:junegunn/fzf
```

Supported target schemes: `gh:user/repo[@tag]`, `gl:user/repo[@tag]`,
`url:https://...`, `apt:pkg`.

## Adding an alias

1. Pick the shard file for the alias's first character.
2. Add one `alias: scheme-target` line (keep entries sorted).
3. Open a pull request. No rebuild of klua is needed — registries are
   fetched at runtime.
