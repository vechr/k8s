# Vechr IIoT

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/vechr-iiot)](https://artifacthub.io/packages/helm/vechr/vechr-iiot)
[![License](https://img.shields.io/github/license/vechr/k8s)](https://raw.githubusercontent.com/vechr/k8s/master/LICENSE)
[![Release](https://img.shields.io/github/release/vechr/k8s.svg)](https://github.com/vechr/k8s/releases/latest)

Have problem ? [Submit an Issue](https://github.com/vechr/k8s/issues)
### Install Cert Manager for Issue the Certificate
```bash
> helm repo add jetstack https://charts.jetstack.io
> helm repo update
> helm install \
    cert-manager jetstack/cert-manager \
    --namespace cert-manager \
    --create-namespace \
    --version v1.11.0 \
    --set installCRDs=true
```

### Install Vehcr IIoT application
```sh
> helm repo add vechr https://helm.vechr.com/helm/charts/
> helm repo update

> helm repo list
NAME          	URL 
vechr          	https://helm.vechr.com/helm/charts/

> helm install vechr-production vechr/vechr-iiot -n production --create-namespace
```

## Persistence Data
You have two choices for storing the data, vechr iiot use postgresql and influxdb to store streaming data and metadata. By default vechr iiot used internal postgresql and influxdb. But you can use external postgresql and influxdb with disabled the option postgresql and influx.

```yaml
# Disabling internal postgresql
postgresql:
  enabled: false

# Disabling internal influxdb
influx:
  enabled: false

# you need to specify port in each microservices
microservices:
  -
    enabled: true
    name: auth-service

    ... please refer to default yaml
    
    # you need this setup this!
    db:
      serviceName: postgres-service
      username: vechrUser
      password: vechr123
      port: 5432

    ... please refer to default yaml
  -
    enabled: true
    name: db-logger-service
    
    ... please refer to default yaml

    # you need this setup this!
    influx:
      serviceName: influx-service
      port: 8086

    ... please refer to default yaml
  -
    enabled: true
    name: notification-service
    
    ... please refer to default yaml
    
    # you need this setup this!
    db:
      serviceName: postgres-service
      username: vechrUser
      password: vechr123
      port: 5432

    ... please refer to default yaml
  -
    enabled: true
    name: things-service
    
    ... please refer to default yaml

    # you need this setup this!
    db:
      serviceName: postgres-service
      username: vechrUser
      password: vechr123
      port: 5432

    ... please refer to default yaml
  
serviceExternal:
  services:
    - name: gmail-service
      enabled: true
      externalName: smtp.gmail.com
      ports:
        - port: 587
    - name: postgres-service # you need this setup this!
      enabled: true
      externalName: host.docker.internal # You need pointing into your postgres host db
      ports:
        - port: 5432 # You need pointing into your postgre port
    - name: influx-service # you need this setup this!
      enabled: true
      externalName: host.docker.internal # You need pointing into your influx host db
      ports:
        - port: 8086 # You need pointing into your influx port
    - name: redis-ext-service # you need this setup this!
      enabled: true
      externalName: host.docker.internal # You need pointing into your redis host db
      ports:
        - port: 6379 # You need pointing into your redis port
```

### You run with option external influxdb and postgres locally and you have docker.
You can use docker for setup PostgreSQL and InfluxDB if you don't have the Server PostgreSQL and InfluxDB running in the cloud.

- Setup PostgreSQL using Docker
  ```bash
  docker run --name db-vechr -e POSTGRES_PASSWORD=vechr123 -e POSTGRES_USER=vechrUser -d -p 5432:5432 postgres
  ```

- Setup InfluxDB using Docker
  ```bash
  # Create folder for storing InfluxDB
  mkdir influx-data
  cd influx-data

  # Run InfluxDB instance
  docker run -d -p 8086:8086 \
        --name influx-vechr \
        -v $PWD/data:/var/lib/influxdb2 \
        -v $PWD/config:/etc/influxdb2 \
        -e DOCKER_INFLUXDB_INIT_MODE=setup \
        -e DOCKER_INFLUXDB_INIT_USERNAME=admin \
        -e DOCKER_INFLUXDB_INIT_PASSWORD=vechr123 \
        -e DOCKER_INFLUXDB_INIT_ORG=Vechr \
        -e DOCKER_INFLUXDB_INIT_BUCKET=Vechr \
        -e DOCKER_INFLUXDB_INIT_ADMIN_TOKEN=vechr-token \
        influxdb:2.1.0-alpine
  ```