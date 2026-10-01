# TechNexion Linux Kernel Overlay for Intel Panther Lake

This repository contains the kernel configuration, out-of-tree patches, and
build scripts used by TechNexion to build Linux kernel packages for Intel
Panther Lake camera platforms.

It is primarily consumed by
[tn-intel-camera-deploy](https://github.com/TechNexion-Vision/tn-intel-camera-deploy)
when building a complete IPU7 camera deployment bundle.

This repository does not contain or maintain the complete Linux kernel source.
The build script downloads the upstream Linux kernel source and applies the
configuration and patches provided here.

## Repository Contents

- `kernel-patches/` — out-of-tree patches applied with Quilt
- `kernel-config/` — base, feature, and platform kernel configurations
- `build.sh` — kernel source preparation, patching, build, and Debian packaging
- `config.sh` — upstream kernel version and build configuration

## Branches

| Branch | Purpose |
|---|---|
| `main` | Standard TechNexion Panther Lake camera kernel |
| `lexcom` | Lexcom-specific Panther Lake camera kernel |

The selected branch must match the branch used by
`tn-intel-camera-deploy`.

## Recommended Usage

Normally, this repository does not need to be cloned or built manually.
Use the matching branch of `tn-intel-camera-deploy`:

```bash
git clone https://github.com/TechNexion-Vision/tn-intel-camera-deploy.git
cd tn-intel-camera-deploy
./ptl-camera.sh --all
```

The deployment script automatically clones the correct kernel overlay branch,
builds the kernel Debian package, and includes it in the final deployment
bundle.

## Direct Kernel Build

For standalone kernel development:

```bash
./build.sh \
  -r no \
  -t <build-tag> \
  -b <build-number> \
  -c <kernel-suffix>
```

Generated kernel Debian packages are placed in the repository root after a
successful build.

## License

The downloaded Linux kernel source and the patches in this repository remain
subject to their respective upstream licenses.
