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
export IMAGE_TAG=v1.1

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
kubectl apply -f ./k8s/mongodb.yaml
kubectl apply -f ./k8s/data-api.yaml
kubectl apply -f ./k8s/flights-api.yaml
kubectl apply -f ./k8s/quakes-api.yaml
kubectl apply -f ./k8s/weather-api.yaml
kubectl apply -f ./k8s/service-tracker-ui.yaml
```

### Hydra

```
kubectl apply -f ./hydra/tracker-db-component.yaml
kubectl apply -f ./hydra/tracker-api-components.yaml
kubectl apply -f ./hydra/tracker-ui-component.yaml

kubectl apply -f ./hydra/tracker-app-config.yaml

kubectl delete -f ./hydra/tracker-app-config.yaml
kubectl delete -f ./hydra/tracker-api-components.yaml
kubectl delete -f ./hydra/tracker-db-component.yaml
kubectl delete -f ./hydra/tracker-ui-component.yaml
```