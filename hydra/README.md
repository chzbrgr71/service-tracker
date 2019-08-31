## Service Tracker Example

### Pre-requisites

* Create Azure Cosmos DB
* Create Azure App Insights


### Deploy

* Deploy

```bash
kubectl create -f tracker-components.yaml
kubectl create -f tracker-app-config.yaml

kubectl delete -f tracker-app-config.yaml
kubectl delete -f tracker-components.yaml
```