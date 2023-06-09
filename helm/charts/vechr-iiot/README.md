# Vechr IIoT


[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/vechr-iiot)](https://artifacthub.io/packages/helm/vechr/vechr-iiot)
[![License](https://img.shields.io/github/license/vechr/k8s)](https://raw.githubusercontent.com/vechr/k8s/master/LICENSE)
[![Release](https://img.shields.io/github/release/vechr/k8s.svg)](https://github.com/vechr/k8s/releases/latest)

Have problem ? [Submit an Issue](https://github.com/vechr/k8s/issues)

Install Cert Manager for Issue the Certificate
```bash
# Install Cert Manager first (if needed)
helm repo add jetstack https://charts.jetstack.io
helm repo update
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.11.0 \
  --set installCRDs=true
```

Install Vehcr IIoT application
```sh
> helm repo add vechr https://vechr.github.io/k8s/helm/charts/
> helm repo update

> helm repo list
NAME          	URL 
vechr          	https://vechr.github.io/k8s/helm/charts/

> helm install vechr-production vechr/vechr-iiot
```