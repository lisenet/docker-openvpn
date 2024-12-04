# OpenVPN for Docker

[![version](https://img.shields.io/github/manifest-json/v/lisenet/docker-openvpn?label=OpenVPN)](https://github.com/lisenet/docker-openvpn/blob/master/manifest.json)
[![Docker Stars](https://img.shields.io/docker/stars/lisenet/openvpn.svg)](https://hub.docker.com/r/lisenet/openvpn/)
[![Docker Pulls](https://img.shields.io/docker/pulls/lisenet/openvpn.svg)](https://hub.docker.com/r/lisenet/openvpn/)
[![last commit](https://img.shields.io/github/last-commit/lisenet/docker-openvpn)](https://github.com/lisenet/docker-openvpn/commits/master)
[![commit activity](https://img.shields.io/github/commit-activity/y/lisenet/docker-openvpn)](https://github.com/lisenet/docker-openvpn/commits/master)
[![issues](https://img.shields.io/github/issues/lisenet/docker-openvpn)](https://github.com/lisenet/docker-openvpn/issues)
[![pull_requests_closed](https://img.shields.io/github/issues-pr-closed/lisenet/docker-openvpn)](https://github.com/lisenet/docker-openvpn/pulls)

OpenVPN server in a Docker container complete with an EasyRSA PKI CA.

Dockerfile and config forked from a no longer maintained [kylemanna/docker-openvpn](https://github.com/kylemanna/docker-openvpn) GitHub repo.

## Upstream Links

* Docker Registry: [lisenet/openvpn](https://hub.docker.com/r/lisenet/openvpn/)
* GitHub: [lisenet/docker-openvpn](https://github.com/lisenet/docker-openvpn)
* OpenVPN: [OpenVPN/openvpn](https://github.com/OpenVPN/openvpn/tags)

## Deprecations

Note that `iptables-legacy` is no longer supported by this repository.

## Release Process

There are three Docker tags used for every new container image build using GitHub workflows:

1. ${OPENVPN_VERSION}
2. ${OPENVPN_VERSION}-build${BUILD_ID}
3. latest

Each build includes the OpenVPN version tag that the image was built with, e.g. `2.6.6`. This image, however, gets updated with every pull request, meaning that it's still a moving target for a given version of OpenVPN.

In order to preserve builds across pulls requests, each release also includes a build ID, e.g. `2.6.6-build12`, which does not get overwritten. If you want to use a specific version of the OpenVPN image that does not change, use this tag.

Finally, each new build updates the `latest` tag, meaning that if you want to use the latest version of the OpenVPN image including all latest code changes, then you should use this tag.

## How to Build Locally

```bash
docker build --pull --no-cache -t lisenet/openvpn:latest .
```

## How to Deploy

Deployment to Kubernetes is currently the only supported (and tested) method. If you would like to [contribute](CONTRIBUTING.md) and provide instructions for other deployment methods (e.g. Podman, Docker engine, Compose, Swarm etc), please consider raising a pull request.

See [docs/kubernetes-deployment.md](./docs/kubernetes-deployment.md).

## Tested On

* OpenVPN server deployment:
  * Kubernetes 1.28 on Rocky 9 (QEMU/KVM).
  * Kubernetes 1.26 on Rocky 8 (QEMU/KVM).
* Clients:
  * Android App OpenVPN Connect 3.3.4 (9290).
  * OpenVPN 2.5.9 on Rocky 9.
  * OpenVPN 2.4.12 on Rocky 8.
  * OpenVPN 2.4.7 on Debian 10.
  * OpenVPN 2.5.5 on Ubuntu 22.04 LTS.
  * OpenVPN 2.4.7 on Ubuntu 20.04 LTS.

## Contributing

[CONTRIBUTING](./CONTRIBUTING.md)

## License

[LICENSE](./LICENSE)

