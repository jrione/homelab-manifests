# TUTORIAL HOW-TO

Install prometheus via Helm just like this:

1. Add helm repo prometheus
    ```bash
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    ```
2. Install prometheus and node-exporter
    ```bash
    helm upgrade prometheus oci://ghcr.io/prometheus-community/charts/prometheus --install -n monitoring --create-namespace -f values.yaml
    ```
3. (Optional) Install Blackbox Exporter
    ```bash
    helm upgrade --install blackbox-exporter oci://ghcr.io/prometheus-community/charts/prometheus-blackbox-exporter -n observability
    ```
    > Harus tambah ini kalo di OpenShift/OKD:
    ```sh 
    oc adm policy add-scc-to-user hostnetwork -z  blackbox-exporter-prometheus-blackbox-exporter -n observability
    ```