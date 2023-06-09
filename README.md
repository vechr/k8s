<img width="2487" alt="Screen Shot 2020-10-12 at 4 59 32 PM" src="https://raw.githubusercontent.com/vechr/k8s/master/images/vechrk8s.svg">
<br>

![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
[![Licence](https://img.shields.io/github/license/vechr/k8s?style=for-the-badge)](./LICENSE)


## Getting started with NATS using Helm

In this repo you can find the Helm 3 based [charts](https://github.com/nats-io/k8s/tree/main/helm/charts) to install Vechr.

```sh
> helm repo add vechr https://vechr.github.io/k8s/helm/charts/
> helm repo update

> helm repo list
NAME          	URL 
vechr          	https://vechr.github.io/k8s/helm/charts/

> helm install production vechr/vechr-iiot
```