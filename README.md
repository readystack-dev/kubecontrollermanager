# kube-controller-manager: ReadyStack build kit

The offline build kit for the Docker image `readystack/kubecontrollermanager:v1.36.6-CE-ubuntu24.04-r5`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v1.36.6-CE-ubuntu24.04-r5](https://github.com/readystack-dev/kubecontrollermanager/releases/tag/v1.36.6-CE-ubuntu24.04-r5)
- Image: [`docker.io/readystack/kubecontrollermanager:v1.36.6-CE-ubuntu24.04-r5`](https://hub.docker.com/r/readystack/kubecontrollermanager/tags), manifest digest `sha256:fda07796c30e074dab71237681287d60d0cb10418b6645077ae2e006e3aa2043`
- Product page: https://readystack.dev/products/kubecontrollermanager
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=kubecontrollermanager

kube-controller-manager is distributed under its upstream licence (Apache-2.0); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [v1.36.6-CE-ubuntu24.04-r5 release](https://github.com/readystack-dev/kubecontrollermanager/releases/tag/v1.36.6-CE-ubuntu24.04-r5): `ReadyStack-kubecontrollermanager-v1.36.6-CE-ubuntu24.04-r5.tar.gz` (501.5 MB), SHA-256 `c9bd5138b8ae1c2bf6ff5af52993e08469f48c7a84041972f1cba1f851671be1`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-kubecontrollermanager-v1.36.6-CE-ubuntu24.04-r5.rebuild.json.sigstore ReadyStack-kubecontrollermanager-v1.36.6-CE-ubuntu24.04-r5.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-kubecontrollermanager-v1.36.6-CE-ubuntu24.04-r5.tar.gz
cd v1.36.6-CE-ubuntu24.04-r5
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-kubecontrollermanager-v1.36.6-CE-ubuntu24.04-r5.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/kubecontrollermanager/recipe. The complete kit is the release download. Each release is a tag here.
