# AskLibra Payment Release

Release assets for the AskLibra Payment Agent appliance.

Source code lives in `shura-tech/asklibra-payment-agent`. This repository is intentionally assets-only and is the update source used by deployed Orange Pi payment hubs.

## Release contract

Each application release uses a tag such as `v0.1.0` and attaches exactly these generated assets:

```text
asklibra-payment-agent-0.1.0.tar.gz
asklibra-payment-agent-0.1.0.sha256
update-manifest.json
```

The installed agent checks:

```text
https://github.com/shura-tech/asklibra-payment-release/releases/latest/download/update-manifest.json
```

The manifest contains the application version, package URL, SHA-256 digest, release notes, and reboot requirement. Payment hubs verify the package digest before installation.

## Publishing

Build release assets from the matching `asklibra-payment-agent` source commit/branch:

```bash
bash scripts/build-release-package.sh
```

Verify:

```bash
cd dist
sha256sum -c asklibra-payment-agent-<version>.sha256
cat update-manifest.json
```

Create a GitHub Release in this repository with tag `v<version>` and upload all three generated files. Do not upload source-repository archives as updater payloads.

Never replace an already-published version with different bytes. If code changes, publish a new version.

## Full SD-card images

Full Orange Pi images are separate from application OTA releases. The source repository's image builder creates the flashable appliance image. This repository is for application update assets only.
