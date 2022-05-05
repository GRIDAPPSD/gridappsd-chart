This chart was created by Kompose

Requires:
  - minikube
  - helm

```
minikube start

helm install gridappsd gridappsd/

kubectl port-forward viz-76f469db57-2b85k 8080:8082 &
kubectl port-forward gridappsd-678964d59c-8xvz8 61613:61613 &
kubectl port-forward gridappsd-678964d59c-8xvz8 61614:61614 &
kubectl port-forward influxdb-cb9d44bd6-k459m 8086:8086 &
kubectl port-forward proven-7694447db7-5fbdr 18080:8080 &

kubectl exec --stdin --tty gridappsd-678964d59c-8xvz8 -- /bin/bash

helm upgrade gridappsd gridappsd/

helm uninstall gridappsd gridappsd/

# stop port forwarding
pkill kubectl

minikube stop
```

## Need platform updates to get communications
  * in goss-gridapps-d if the variable PROVEN_ENDPOINT is defined use the variable version, if not then use http://localhost:18080
  * may also need for blazegraph
