# SIEM-kubernetes

```
# install the helm chart
cd SIEM-kubernetes
helm install siem .

# upgrade the helm chart
helm upgrade siem .

# uninstall the helm chart (default ns)
helm uninstall siem
```

## Ping Snort
```
# get pods ip address
kubectl get pods -n monitoring
kubectl describe pod -n monitoring snort-<pods-id>
# Or
kubectl get pods -n monitoring -o wide

# ping the pod
kubectl exec -it -n monitoring test-ping -- /bin/sh
/# ping <snort-pod-ip>

# check the logs
kubectl logs -n monitoring snort-<pods-id>
```