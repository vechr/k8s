### Create Cluster Kubernetes for testing
You can check the list of [kindest/node](https://hub.docker.com/r/kindest/node/tags?page=1&ordering=name). And for the documentation you can see this [pages](https://kind.sigs.k8s.io/).

```bash
cd cluster
kind create cluster --name vechr-cluster --image kindest/node:v1.25.9 --config kind.yaml
```

### Setup Load Balancer for Kind
```bash
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.7/config/manifests/metallb-native.yaml

kubectl wait --namespace metallb-system \
                --for=condition=ready pod \
                --selector=app=metallb \
                --timeout=90s

docker network inspect -f '{{.IPAM.Config}}' kind

kubectl apply -f https://kind.sigs.k8s.io/examples/loadbalancer/metallb-config.yaml
```

### If you already have images
You can load your local images to kind cluster, sometimes kind cluster slow during pulling images

```bash
kind load docker-image asia-southeast2-docker.pkg.dev/vechr-iiot-389413/vechr-iiot-repository/web-app \
  asia-southeast2-docker.pkg.dev/vechr-iiot-389413/vechr-iiot-repository/audit-service \
  asia-southeast2-docker.pkg.dev/vechr-iiot-389413/vechr-iiot-repository/auth-service \
  asia-southeast2-docker.pkg.dev/vechr-iiot-389413/vechr-iiot-repository/things-service \
  asia-southeast2-docker.pkg.dev/vechr-iiot-389413/vechr-iiot-repository/notification-service \
  asia-southeast2-docker.pkg.dev/vechr-iiot-389413/vechr-iiot-repository/db-logger-service \
  nats:2.9.17-alpine \
  influxdb:2.1.0-alpine \
  --name vechr-cluster
```

### Access the Ingress
You need to port forwarding the Ingress service
```bash
sudo kubectl port-forward -n your-namespace service/your-nginx-service 443:443
sudo kubectl port-forward -n your-namespace service/nats-lb 9090:9090 4222:4222 1833:1833
```