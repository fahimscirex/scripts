# scripts

Small, dependency-light maintenance tools for Arch Linux. Each tool lives in
its own folder with its own README. Both are single-file bash scripts, both
are Arch-only.

| Folder        | Tool        | What it does |
|---------------|-------------|--------------|
| `rank/`       | `rank`      | Benchmarks pacman mirrors with `rate-mirrors` and atomically updates mirrorlists, with backups and restore. |
| `archclean/`  | `archclean` | Reports and reclaims disk space from package caches, logs, user caches and toolchain caches. Safe by default: scanning never deletes anything. |

## License

GPL-3.0 — see [LICENSE](LICENSE).
