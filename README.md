<p align="center">
  <a href="" target="blank"><img src="https://raw.githubusercontent.com/vechr/k8s/master/images/vechrk8s.svg" width="350" alt="Vechr k8s" /></a>
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
  <a href="https://artifacthub.io/packages/search?repo=vechr">
    <img alt="Artifact Hub" src="https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/vechr">
  </a>
  <a href="https://raw.githubusercontent.com/vechr/k8s/master/LICENSE">
    <img alt="License" src="https://img.shields.io/github/license/vechr/k8s">
  </a>
</p>


## Getting started with Vechr IIoT using Helm

In this repo you can find the Helm 3 based [charts](https://github.com/vechr/k8s/tree/master/helm/charts) to install Vechr.

### Install Helm Repository
```sh
> helm repo add vechr https://helm.vechr.com/helm/charts/
> helm repo update

> helm repo list
NAME          	URL 
vechr          	https://helm.vechr.com/helm/charts/
```