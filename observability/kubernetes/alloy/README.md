# HOWTO:

1. Setup helm (install, add repo, dsb)
```
helm repo add grafana https://grafana.github.io/helm-charts
```

2. Create custom configmap
```
kubectl create namespace observability
```
```
kubectl create configmap alloy-configmap -n observability --from-file=config.alloy --dry-run=client -oyaml | kubectl apply -f -
```

3. Install Alloy via Helm
```
helm upgrade  --namespace observability alloy grafana/alloy -f values.yaml
``` 

