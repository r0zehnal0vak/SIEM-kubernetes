# SIEM-kubernetes

```
# install the helm chart
cd SIEM-kubernetes
helm install siem .
```

## Ping Snort
```
# get pods ip address
kubectl get pods -n monitoring
kubectl describe pod -n monitoring snort-<pods-id>

# ping the pod
kubectl exec -it -n monitoring test-ping -- /bin/sh
/# ping <snort-pod-ip>

# check the logs
kubectl logs -n monitoring snort-<pods-id>
```

## Install with Loki-stack
```
helm install siem . -n monitoring --create-namespace

helm upgrade siem . -n monitoring

helm list -n monitoring

helm uninstall siem -n monitoring
```