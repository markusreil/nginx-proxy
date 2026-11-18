# nginx-proxy-hardened

[![version](https://img.shields.io/docker/v/mreil/nginx-proxy-hardened?sort=semver&logo=docker)](https://hub.docker.com/r/mreil/nginx-proxy-hardened/tags)
Hardened Alpine build of [nginx-proxy/nginx-proxy](https://github.com/nginx-proxy/nginx-proxy).
For usage and general documentation, see the [upstream README](https://github.com/nginx-proxy/nginx-proxy/blob/main/README.md)
and [docs](https://github.com/nginx-proxy/nginx-proxy/tree/main/docs).

Published images: [`mreil/nginx-proxy-hardened`](https://hub.docker.com/r/mreil/nginx-proxy-hardened)
(`:1.11.1-alpine-hardened.1`, `:alpine`).

```shell
docker run --detach \
    --name nginx-proxy \
    --publish 80:80 \
    --volume /var/run/docker.sock:/tmp/docker.sock:ro \
    mreil/nginx-proxy-hardened:alpine
```

## What changed vs upstream

- `Dockerfile.alpine`: nginx base bumped to `1.31.9-alpine`; `zlib` upgraded (CVE-2026-4738).
- `docker-gen` (0.17.2) and `forego` (0.18.8) are compiled from source with a current
  Go toolchain instead of copied from their published images, whose old Go releases
  carried most of the reported CVEs. Trivy reports **0 vulnerabilities** for the image.
- `.github/workflows/build-publish.yml`: pushes and schedules removed; publishing is
  manual (`workflow_dispatch`) only.
