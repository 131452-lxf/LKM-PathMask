# TODO

## Multi-path hiding

Status: implemented.

Current behavior:

- `target_path` remains available for a legacy single path.
- `target_paths` accepts comma-separated paths.
- The KernelSU wrapper accepts one path per line in `target_path.conf`.
- Each existing path is resolved to a `(dev, inode)` pair at module load time.
- Missing paths are skipped; loading fails only if no configured path exists.

Follow-up ideas:

- Add duplicate target detection.
- Add a runtime debug log that prints the number of hidden entries removed from
  each `getdents64` buffer.

## Scoped hiding / blacklist / whitelist

Status: implemented for UID blacklist and whitelist.

Current behavior:

- `scope_mode=global` keeps the old behavior.
- `scope_mode=deny` hides only from configured UIDs.
- `scope_mode=allow` hides from everyone except configured UIDs.
- The KernelSU wrapper resolves package names from `deny_packages.conf` or
  `allow_packages.conf` into UIDs before loading the module, based on the
  active scope mode.
- The KernelSU WebUI can edit paths, scoped packages, direct UIDs,
  `scope_mode`, and `hide_dirents`.

Follow-up ideas:

- Add process-name matching as a secondary filter.
- Add runtime config updates without unload/reload.
