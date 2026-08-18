# OpenVPN Server Deployment with Docker Compose

OpenVPN server in a container running with Docker Compose.

## Pre-requisites

1. Docker Engine with Docker Compose plugin.
2. A public DNS name or IP address for the OpenVPN server.

### Docker Engine on Ubuntu

Follow the official [Docker Engine installation guide for Ubuntu](https://docs.docker.com/engine/install/ubuntu/#prerequisites).

## Copy Docker Compose File

Copy [docker-compose.yml](../docker-compose.yml) to the target server.

## Configure Docker Compose

Edit [docker-compose.yml](../docker-compose.yml) and set `VPN_HOSTNAME` in the `generate-config` service:

```yaml
VPN_HOSTNAME: vpn.example.com
```

Update the other variables in `docker-compose.yml` if you need to change the port, protocol, DNS server, or VPN network.

## Generate OpenVPN Configuration Files and Certificates

Generate the OpenVPN server config. The server config files are created in `./ovpn0`:

```bash
docker compose run --rm generate-config
docker compose run --rm init-pki
docker compose run --rm copy-server-files
```

Start the OpenVPN server:

```bash
docker compose up -d openvpn
```

The `init-pki` step is interactive because it asks for the CA password. For a fully non-interactive but less secure setup, run:

```bash
docker compose run --rm init-pki ovpn_initpki nopass
```

## Create a Client

Generate a client configuration:

```bash
CLIENT_NAME=laptop0 docker compose run --rm add-client
```

The generated client file is written to:

```text
ovpn0/laptop0.ovpn
```
