### Install Vehcr Monitoring Tool
```sh
> helm repo add vechr https://helm.vechr.com/helm/charts/
> helm repo update

> helm repo list
NAME          	URL 
vechr          	https://helm.vechr.com/helm/charts/

> helm install vechr-monitoring vechr/vechr-monitoring -n monitoring --create-namespace
```