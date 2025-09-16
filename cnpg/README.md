# INSTALLATION HOWTO:

Install CNPG cukup ez, berikut stepnya

1. Nambahin helm repo untuk install cnpg controller

   ```shell
   helm repo add cnpg https://cloudnative-pg.github.io/charts
   helm repo update
   helm install cnpg cnpg/cloudnative-pg   --namespace cnpg-system   --create-namespace
   ```
2. Create secret for superuser db (bebas lah)

   ```yaml
   kubectl create secret generic cnpg-cluster-superuser -n database \
     --from-literal=username=postgres \
     --from-literal=password=SuperSecretPass123
   ```
3. Create manifest kind cluster seperti berikut:

   ```yaml
      apiVersion: postgresql.cnpg.io/v1
      kind: Cluster
      metadata:
        name: cnpg-cluster
        namespace: database
      spec:
        instances: 1
        imageName: ghcr.io/cloudnative-pg/postgresql:16.4
        storage:
          storageClass: nfs-client
          size: 8Gi
        bootstrap:
          initdb:
            database: appdb
            owner: appuser
            secret:
              name: appuser-secret
   ```

3. Execute dengan `kubectl apply -f cluster.yaml`
