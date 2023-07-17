# OpenVPN for Docker

[![Docker Stars](https://img.shields.io/docker/stars/lisenet/openvpn.svg)](https://hub.docker.com/r/lisenet/openvpn/)
[![Docker Pulls](https://img.shields.io/docker/pulls/lisenet/openvpn.svg)](https://hub.docker.com/r/lisenet/openvpn/)

OpenVPN server in a Docker container complete with an EasyRSA PKI CA.

Dockerfile and config forked from no longer maintained GitHub repo: https://github.com/kylemanna/docker-openvpn

## Upstream Links

* Docker Registry: [lisenet/openvpn](https://hub.docker.com/r/lisenet/openvpn/)
* GitHub: [lisenet/docker-openvpn](https://github.com/lisenet/docker-openvpn)

## How to Build Locally

```bash
docker build --pull --no-cache -t lisenet/openvpn:latest .
```

## Tested On

* Docker hosts:
  * QEMU/KVM server running Rocky Linux 8/9.
* Clients:
  * Android App OpenVPN Connect 3.3.4 (9290).

## License

[LICENSE](./LICENSE)

