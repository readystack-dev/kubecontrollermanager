[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Fkubecontrollermanager-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/kubecontrollermanager) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/kubecontrollermanager)](https://hub.docker.com/r/readystack/kubecontrollermanager) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/kubecontrollermanager) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

# kube-controller-manager: ReadyStack build kit

The offline build kit for the Docker image `readystack/kubecontrollermanager:v1.36.6-CE-ubuntu24.04-r5`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v1.36.6-CE-ubuntu24.04-r5](https://github.com/readystack-dev/kubecontrollermanager/releases/tag/v1.36.6-CE-ubuntu24.04-r5)
- Image: [`docker.io/readystack/kubecontrollermanager:v1.36.6-CE-ubuntu24.04-r5`](https://hub.docker.com/r/readystack/kubecontrollermanager/tags), manifest digest `sha256:fda07796c30e074dab71237681287d60d0cb10418b6645077ae2e006e3aa2043`
- Product page: https://readystack.dev/products/kubecontrollermanager
- Source and build recipe: https://readystack.dev/products/kubecontrollermanager/recipe
- Build trail: https://readystack.dev/products/kubecontrollermanager/trail/v1.36.6-CE-ubuntu24.04-r5
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=kubecontrollermanager

## The image

One binary per image, as upstream's images: /usr/local/bin/kube-controller-manager, started by kubeadm's static Pod manifest /etc/kubernetes/manifests/kube-controller-manager.yaml (command: kube-controller-manager --kubeconfig=/etc/kubernetes/controller-manager.conf ...). The ENTRYPOINT is /go-runner (upstream's kube-log-runner); a Pod command replaces it. In the Kubernetes VM Stack it is mirrored into the local registry as <LOCAL_REGISTRY>/kube-controller-manager:v1.36.6 and kubeadm pulls it from there.

## Who uses kube-controller-manager and why

Cluster administrators and platform engineers who build and run their own Kubernetes control plane.

kube-controller-manager runs the control loops built into Kubernetes. Each controller watches the cluster's state through the API server and makes changes that move the current state towards the desired state.

A typical use: A team asks for several replicas of a web server. When a node fails and its pods disappear, a controller in kube-controller-manager sees fewer replicas than requested and creates replacements; other controllers keep namespaces, endpoints and service accounts in line, without an operator stepping in.

From the upstream project's own description: https://kubernetes.io/docs/reference/command-line-tools-reference/kube-controller-manager/, https://kubernetes.io/docs/concepts/overview/components/.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-21 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 83 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`999:999`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-21; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/kubecontrollermanager.

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

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/kubecontrollermanager/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev
