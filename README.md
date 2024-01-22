This chart was created by Kompose

Requires:
  - minikube
  - helm

```
minikube start

helm install gridappsd gridappsd/

kubectl port-forward $(kubectl get pods --no-headers -o custom-columns=":metadata.name" | grep gridappsd-platform-viz) 8080:8080 &
kubectl port-forward $(kubectl get pods --no-headers -o custom-columns=":metadata.name" | grep gridappsd-platform-gridappsd) 61613:61613 &
kubectl port-forward $(kubectl get pods --no-headers -o custom-columns=":metadata.name" | grep gridappsd-platform-gridappsd) 61614:61614 &
kubectl port-forward $(kubectl get pods --no-headers -o custom-columns=":metadata.name" | grep gridappsd-platform-influxdb) 8086:8086 &
kubectl port-forward $(kubectl get pods --no-headers -o custom-columns=":metadata.name" | grep gridappsd-platform-proven) 18080:8080 &

kubectl exec --stdin --tty $(kubectl get pods --no-headers -o custom-columns=":metadata.name" | grep gridappsd-platform-gridappsd) -- /bin/bash

helm upgrade gridappsd gridappsd/

helm uninstall gridappsd gridappsd/

# stop port forwarding
pkill kubectl

minikube stop
```

## Need platform updates to get communications
  * in goss-gridapps-d if the variable PROVEN_ENDPOINT is defined use the variable version, if not then use http://localhost:18080
  * may also need for blazegraph
