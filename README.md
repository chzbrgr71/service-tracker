# service-tracker sample app

### Run local

```bash
export MONGODB_USER=dbuser
export MONGODB_PASSWORD=dbpassword
export MONGODB_IP=localhost
export MONGODB_PORT=27017
export MONGODB_PORT=27018

export DATA_SERVICE_URI=http://localhost:3009/
export FLIGHT_API_ROOT=http://localhost:3003/
export WEATHER_API_ROOT=http://localhost:3015/
export QUAKES_API_ROOT=http://localhost:3012/
```

### Docker Images

```bash
export IMAGE_TAG=v1.5

docker build -t chzbrgr71/data-api:$IMAGE_TAG ./app/data-api
docker push chzbrgr71/data-api:$IMAGE_TAG

docker build -t chzbrgr71/flights-api:$IMAGE_TAG ./app/flights-api
docker push chzbrgr71/flights-api:$IMAGE_TAG

docker build -t chzbrgr71/quakes-api:$IMAGE_TAG ./app/quakes-api
docker push chzbrgr71/quakes-api:$IMAGE_TAG

docker build -t chzbrgr71/weather-api:$IMAGE_TAG ./app/weather-api
docker push chzbrgr71/weather-api:$IMAGE_TAG

docker build -t chzbrgr71/service-tracker-ui:$IMAGE_TAG ./app/service-tracker-ui
docker push chzbrgr71/service-tracker-ui:$IMAGE_TAG
```

### Deploy in Kubernetes

```bash
kubectl apply -f ./k8s/mongodb.yaml -n tracker
kubectl apply -f ./k8s/data-api.yaml -n tracker
kubectl apply -f ./k8s/flights-api.yaml -n tracker
kubectl apply -f ./k8s/quakes-api.yaml -n tracker
kubectl apply -f ./k8s/weather-api.yaml -n tracker
kubectl apply -f ./k8s/service-tracker-ui.yaml -n tracker

kubectl delete -f ./k8s/mongodb.yaml
kubectl delete -f ./k8s/data-api.yaml
kubectl delete -f ./k8s/flights-api.yaml
kubectl delete -f ./k8s/quakes-api.yaml
kubectl delete -f ./k8s/weather-api.yaml
kubectl delete -f ./k8s/service-tracker-ui.yaml

kubectl run my-shell -n tracker --rm -i --tty --image ubuntu -- bash
kubectl run my-shell --rm -i --tty --image ubuntu -- bash
apt-get update
apt-get install dnsutils
```

### Hydra

```bash
kubectl apply -f ./hydra/tracker-db-component.yaml
kubectl apply -f ./hydra/tracker-api-components.yaml
kubectl apply -f ./hydra/tracker-ui-component.yaml

kubectl apply -f ./hydra/tracker-app-config.yaml

kubectl delete -f ./hydra/tracker-app-config.yaml
kubectl delete -f ./hydra/tracker-api-components.yaml
kubectl delete -f ./hydra/tracker-db-component.yaml
kubectl delete -f ./hydra/tracker-ui-component.yaml
```

### GitHub Image Registry Commands

```bash
cat ~/TOKEN.txt | docker login https://docker.pkg.github.com -u chzbrgr71 --password-stdin

docker pull chzbrgr71/data-api:v1.1
docker pull chzbrgr71/flights-api:v1.1
docker pull chzbrgr71/quakes-api:v1.1
docker pull chzbrgr71/weather-api:v1.1
docker pull chzbrgr71/service-tracker-ui:v1.1

docker tag bitnami/mongodb:4.0.10-debian-9-r39 docker.pkg.github.com/chzbrgr71/service-tracker/bitnami/mongodb:v1.1
docker tag chzbrgr71/data-api:v1.1 docker.pkg.github.com/chzbrgr71/service-tracker/data-api:v1.1
docker tag chzbrgr71/flights-api:v1.1 docker.pkg.github.com/chzbrgr71/service-tracker/flights-api:v1.1
docker tag chzbrgr71/quakes-api:v1.1 docker.pkg.github.com/chzbrgr71/service-tracker/quakes-api:v1.1
docker tag chzbrgr71/weather-api:v1.1 docker.pkg.github.com/chzbrgr71/service-tracker/weather-api:v1.1
docker tag chzbrgr71/service-tracker-ui:v1.1 docker.pkg.github.com/chzbrgr71/service-tracker/service-tracker-ui:v1.1

docker push docker.pkg.github.com/chzbrgr71/service-tracker/data-api:v1.1
docker push docker.pkg.github.com/chzbrgr71/service-tracker/flights-api:v1.1
docker push docker.pkg.github.com/chzbrgr71/service-tracker/quakes-api:v1.1
docker push docker.pkg.github.com/chzbrgr71/service-tracker/weather-api:v1.1
docker push docker.pkg.github.com/chzbrgr71/service-tracker/service-tracker-ui:v1.1


```