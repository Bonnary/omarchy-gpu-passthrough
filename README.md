# omarchy-gpu-passthrough

GPU passthrough, Looking Glass, and Windows VM tooling, extracted from
[omarchy/omarchy PR #3454](https://github.com/omacom/omarchy/pull/3454)
("GPU passthrough and Windows VM with Looking Glass").

This is the GPU/VM portion only — not the entire Omarchy Linux distribution.

## Contents

- `bin/omarchy-gpu-passthrough` — main dispatcher
- `bin/omarchy-gpu-passthrough-bind` — GPU/vfio driver binding (mode control)
- `bin/omarchy-gpu-passthrough-info` — diagnostics and status
- `bin/omarchy-gpu-passthrough-setup` — one-time setup wizard
- `bin/omarchy-gpu-passthrough-utils` — shared library
- `bin/omarchy-looking-glass-install` — Looking Glass installer
- `bin/omarchy-looking-glass-launch` — Looking Glass client launcher
- `bin/omarchy-windows-passthrough-vm` — Windows VM management (GPU passthrough + Looking Glass)

Installation notes for Omarchy 4+ (`quattro`): these scripts use Omarchy's built-in
`omarchy-snapshot` and `omarchy-version` commands, and are renamed (`*-passthrough-*`)
to avoid shadowing Omarchy 4's official `omarchy-windows-vm` (Docker/RDP VM).

## Quick start

Put `bin/` on your `PATH`, then:

```bash
omarchy-gpu-passthrough info detect     # verify hardware compatibility
omarchy-gpu-passthrough setup           # run setup wizard
sudo reboot                             # apply kernel parameters
omarchy-gpu-passthrough info verify     # confirm configuration
omarchy-windows-passthrough-vm install              # install Windows VM (~20 min)
omarchy-windows-passthrough-vm launch --lg          # launch via Looking Glass
```

See the [PR description](https://github.com/omacom/omarchy/pull/3454) for
full usage, hardware requirements, and known limitations.

## Note on dependencies

These scripts were authored inside Omarchy and may reference other
`omarchy-*` helpers (package install, update, version, etc.) not shipped
here. If you use them on a non-Omarchy system you may need to provide
those helpers or run the commands directly. The core GPU passthrough
logic is self-contained within `bin/`.

## License

MIT — original copyright (c) David Heinemeier Hansson, as in the upstream
repository. Extracted from omarchy by Sławomir Andreasik (PR author).
