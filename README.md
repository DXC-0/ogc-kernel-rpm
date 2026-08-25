# ogc-kernel

Publishes prebuilt RPMs of the OGC kernel for Fedora x86_64, fetched upstream and published via GitHub Actions on a 6-hour cycle.

## About

The [Open Gaming Collective](https://opengamingcollective.org/) is a shared effort to consolidate gaming-related kernel improvements across projects instead of each one maintaining its own separate fork and patch set.

The OGC kernel is based on the upstream Fedora kernel with additional patches targeting handheld and gaming hardware (scheduler tuning, controller/HID fixes, power management for handheld SoCs, etc.).

This repository does not build the kernel. It fetches the prebuilt RPMs and republishes them as GitHub releases. <br/> Artifact extraction pipeline only. Kernel and RPM maintenance is handled by the [OCG](https://github.com/OpenGamingCollective) team.

## Packages

| Package | Description |
|---|---|
| `kernel` | Meta-package, depends on `kernel-core` + `kernel-modules` |
| `kernel-core` | Bootable kernel binary and essential modules |
| `kernel-modules` | Additional loadable kernel modules |
| `kernel-devel` | Headers/files for building external (out-of-tree) modules |
| `kernel-devel-matched` | `kernel-devel` pinned to the currently running kernel version |
| `kernel-headers` | Headers for userspace program compilation |

## Manual installation

Grab the RPMs for the current release from the [releases page](https://github.com/DXC-0/ogc-kernel-rpm/releases/latest).

```bash
curl -LO https://github.com/DXC-0/ogc-kernel-rpm/releases/latest/download/kernel-<version>.rpm
curl -LO https://github.com/DXC-0/ogc-kernel-rpm/releases/latest/download/kernel-core-<version>.rpm
curl -LO https://github.com/DXC-0/ogc-kernel-rpm/releases/latest/download/kernel-modules-<version>.rpm

sudo dnf install ./kernel-*.rpm
```

Add `kernel-devel` (or `kernel-devel-matched`) and `kernel-headers` if you need DKMS or out-of-tree module builds.

### Verifying downloads

Each asset's SHA256 is listed on the release page. Verify before installing:

```bash
sha256sum kernel-core-<version>.rpm
```

Compare against the published digest.

### Verifying the running kernel

Reboot and confirm:

```bash
uname -r
```

## Uninstalling

Do not remove the kernel currently in use.

```bash
sudo dnf remove kernel-<version>
```

## Notes

- This repo is not run by the OGC team.
- For kernel issues/bugs, report them upstream, not here.
- Not affiliated with or endorsed by the Fedora Project.
