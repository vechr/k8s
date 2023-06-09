<p align="center">
  <a href="" target="blank"><img src="https://raw.githubusercontent.com/vechr/k8s/master/images/vechrk8s.svg" width="1000" alt="Vechr k8s" /></a>
  <br>
  <i>Vehcr IIoT is platfom SaaS to help productivity in manufacturing through Technology
    <br> Running in Kubernetes Engine, it can be cloud or on premises.</i>
  <br>
</p>

<p align="center">
  <a href="https://github.com/vechr/k8s/issues">Submit an Issue</a>
  <br>
  <br>
</p>

<p align="center">
  <a href="https://artifacthub.io/packages/helm/vechr/vechr-iiot">
    <img alt="Artifact Hub" src="https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/vechr-iiot">
  </a>
  <a href="https://raw.githubusercontent.com/vechr/k8s/master/LICENSE">
    <img alt="License" src="https://img.shields.io/github/license/vechr/k8s">
  </a>
  <a href="https://github.com/vechr/k8s/releases/latest">
    <img alt="Release" src="https://img.shields.io/github/release/vechr/k8s.svg">
  </a>
</p>

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