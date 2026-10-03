# rank

Map-aware pacman mirror ranking utility. Detects your active repositories
(official Arch plus Chaotic-AUR, ArchLinuxCN, EndeavourOS, CachyOS,
BlackArch, Arch4Edu, Artix, ArcoLinux, Manjaro), benchmarks their mirrors
with `rate-mirrors`, and writes the fastest ones to `/etc/pacman.d/`.

Requirements: an Arch-based distro,
[`rate-mirrors`](https://github.com/westandskif/rate-mirrors), and root
(via sudo) for anything that writes to `/etc/pacman.d/`. `--list` and
`--dry-run` work without root.

```sh
rank                      # detect repos and rank them
rank arch chaotic-aur     # rank specific repos only
rank --dry-run arch       # benchmark without writing anything
rank -f -c DE             # fast mode, entry country Germany
rank --list               # show detected repos and exit
rank --restore            # restore a mirrorlist from backup
```

Behavior worth knowing:

- Every overwritten mirrorlist gets a timestamped backup in
  `/etc/pacman.d/backups/` (last 5 kept) plus a `mirrorlist.bak` next to it.
- Only one instance runs at a time (lock file under `/run/lock`).
- After ranking it offers to refresh pacman databases with `pacman -Syy`
  (double-y on purpose: mirrors just changed, so databases are re-fetched).
- Options: `-m/--max-mirrors 1-100`, `--completion 0-1` (arch only),
  `-y/--yes`, `-s/--sync`, `--no-sync`, `--no-backup`, `--no-color`.

## License

GPL-3.0 — see [../LICENSE](../LICENSE).
