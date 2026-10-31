# Rafael Xray Core

Rafael's IP-limit-enabled Xray Core fork, built for Rafael Panel. The upstream base is [`XTLS/Xray-core`](https://github.com/XTLS/Xray-core) at `v1.260327.0`; Rafael's runtime IP-limit integration is under `xray-core/app/iplimit` and the dispatcher hook.

This repository publishes the matching Linux amd64 Xray binary and source archive. Rafael Panel's release workflow pins a tag and SHA-256, then bundles the verified binary inside `rafael-linux-amd64.tar.gz`; panel users do not need a separate Xray download.

## Build and releases

Pushing a version tag (`v*`) runs the reproducible Linux amd64 build and publishes:

- `rafael-xray-linux-amd64` and its SHA-256 sidecar
- `rafael-xray-core-source.tar.gz` and its SHA-256 sidecar
- The license, notices, and fork version manifest

The build checks the complete source-tree fingerprint before compiling. Go is pinned to 1.26.2. See [`xray-fork-version.txt`](./xray-fork-version.txt) for upstream and fork pins.

## IP limit integration

The panel writes a strict JSON snapshot to the path supplied by `XRAY_IPLIMIT_FILE`. The fork groups multi-link aliases using the shared identity provided by the panel and enforces the strictest positive IP cap across those aliases inside one Xray process. This state is process-local; separate Xray processes do not share live connection state. Running this Xray binary without `XRAY_IPLIMIT_FILE` leaves the IP-limit hook inactive. Traffic coefficients are handled by Rafael Panel and do not change Xray behavior.

## License

The Xray source and Rafael modifications in `xray-core/` are distributed under the upstream Mozilla Public License 2.0. See [`LICENSE`](./LICENSE) and [`NOTICE`](./NOTICE). Third-party dependency licenses remain those specified by their respective projects.
