# archclean

A safe system cleaner for Arch Linux. Reports reclaimable space per category
(`scan`, the default) and deletes only on an explicit `clean` plus
confirmation.

```sh
archclean                        # scan everything
archclean scan cache trash       # scan selected categories
archclean clean --all --dry-run  # preview a full clean
archclean clean pkgcache orphans # trim package cache, drop orphans
archclean clean cache -y         # clear ~/.cache without prompting
```

Categories: `pkgcache` (trimmed with `paccache`, keeps N newest per package —
needs `pacman-contrib`), `orphans` (removed with `pacman -Rs`, keeps user
config files), `crash`, `coredump`, `logs` (journal vacuumed with
`journalctl --vacuum-time`, never `rm`'d), `cache` (allowlist of regenerable
app caches only — never the whole `~/.cache`),
`trash`, `npm`, `npx`, `bun`, `go`, `cargo`, `uv`, plus `claude` and `agy`.

Note: `claude` (old Claude Code versions) and `agy` (old antigravity-cli
binaries) reflect the author's setup — they assume default install paths
(`~/.local/share/claude/versions`, `~/.local/bin`). They are harmless
elsewhere (they just report nothing) but only useful if you use those tools.

Options: `-a/--all`, `-n/--dry-run`, `-y/--yes`, `-x/--exclude GLOB`
(repeatable; applies to crash, cache, trash and coredump), `-k/--keep N`,
`--journal-keep T` (e.g. `10d`, `500M`).

Defaults can live in a config file (parsed, never executed — CLI flags win):

- `/etc/archclean.conf` (system-wide)
- `~/.config/archclean/config` (per-user)

```ini
keep_versions   = 1
journal_keep    = 2weeks
exclude         = mozilla, *.pacnew
cache_allowlist = thumbnails, fish, pip
assume_yes      = false
dry_run         = false
```

`cache_allowlist` replaces the default `cache` allowlist (omit the key to
keep the defaults; use `exclude` to subtract single entries instead). The
special value `ALL` restores whole-directory cleaning.

## License

GPL-3.0 — see [../LICENSE](../LICENSE).
