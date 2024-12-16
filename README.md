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
# This may throw errors, but the installation will proceed.
# The error occurs due to the --create-namespace flag, which is required for now
# because Loki uses {{ .Release.namespace }}. ## TODO  ##

helm install siem . -n monitoring --create-namespace

helm upgrade siem . -n monitoring

helm list -n monitoring

helm uninstall siem -n monitoring
```