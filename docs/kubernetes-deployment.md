# OpenVPN Server Deployment on Kubernetes

OpenVPN server in a container running on Kubernetes.

## Pre-requisites

1. Docker engine on a host where OpenVPN configuration is to be created (e.g. your laptop).
2. A running Kubernetes cluster with ingress to use `LoadBalancer` service type.
3. Kubectl access to the Kubernetes cluster.

### Docker Engine on Ubuntu

Use this to install Docker engine if your host is running on Ubuntu:

```bash
sudo apt install -y curl git software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository -y "deb https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update -qq
sudo apt install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
```

### Docker Engine on CentOS/Rocky

Use this to install Docker engine if your host is running on CentOS/Rocky:

```bash
sudo yum install -y git yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
```

## Clone This Repository

```bash
git clone https://github.com/lisenet/docker-openvpn.git
cd ./docker-openvpn
```

## Generate OpenVPN Configuration Files and Certificates

Set environment variables to be used to generate OpenVPN server config.

Note that the `VPN_PORT` variable here is used for Kubernetes service only. Inside the pod, the container port is always 1194.

```bash
export VPN_HOSTNAME="vpn.example.com"
export VPN_PORT="31194"
export VPN_PROTOCOL="tcp"
export DNS_SERVER="8.8.8.8"
export NETWORK_CIDR="10.8.0.0/24"
export NAMESPACE="openvpn"
```

Generate basic OpenVPN config:

```bash
./bin/generate-config.sh
```

Change ownership of `ovpn0` folder so that we can write to it:

```bash
sudo chown -R "${USER}:${USER}" ./ovpn0/
```

Generate a client config (can be repeated for any new client):

```bash
export CLIENT_NAME=android
./bin/add-client.sh
```

## Create Kubernetes Secrets

This will create a Kubernetes namespace as well as write secrets to it.

Prepend with `REPLACE=true` to update the existing ones:

```bash
./bin/set-secrets.sh
```

## Deploy OpenVPN Server to Kubernetes

This will deploy an OpenVPN server to Kubernetes and create a `LoadBalancer` type service so that you can access it externally. If you do not have ingress configured on your cluster, you can manually modify the YAML file to change the service type to use a `NodePort` instead.

```bash
kubectl apply -f ./deployment/openvpn-kubernetes.yml
```

Get the Kubernetes service load balancer IP address:

```bash
kubectl get svc -n openvpn
NAME      TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)           AGE
openvpn   LoadBalancer   10.98.140.199   10.11.1.53    31194:31292/TCP   73m
```

Check pod logs:

```bash
kubectl -n openvpn logs $(kubectl -n openvpn get pods -o name)
```

