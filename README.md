# SIEM-kubernetes

```
# install the helm chart
cd SIEM-kubernetes
helm install siem .
```

## Ping Snort
```
# get pods ip address
kubectl describe pod -n monitoring snort-<pods-id>

# ping the pod
kubectl exec -it -n monitoring test-ping -- /bin/sh
/# ping <snort-pod-ip>

# check the logs
kubectl logs -n monitoring snort-<pods-id>
```
