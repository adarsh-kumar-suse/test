
helm repo add suse-observability https://charts.rancher.com/server-charts/prime/suse-observability
helm repo update


export VALUES_DIR=.
helm template \
  --set license='your key' \
  --set baseUrl='http://observability.internal.suse.com' \
  --set sizing.profile='trial' \
  suse-observability-values \
  suse-observability/suse-observability-values --output-dir $VALUES_DIR


export VALUES_DIR=.
helm upgrade --install \
    --namespace suse-observability \
    --create-namespace \
    --values $VALUES_DIR/suse-observability-values/templates/baseConfig_values.yaml \
    --values $VALUES_DIR/suse-observability-values/templates/sizing_values.yaml \
    --values $VALUES_DIR/suse-observability-values/templates/ingress_values.yaml \
    --values $VALUES_DIR/suse-observability-values/templates/affinity_values.yaml \
    suse-observability \
    suse-observability/suse-observability


-----------ingress_values.yaml------------
ingress:
  annotations:
    nginx.ingress.kubernetes.io/proxy-body-size: "50m"
    nginx.ingress.kubernetes.io/proxy-read-timeout: '3600'
    nginx.ingress.kubernetes.io/proxy-sent-timeout: '3600'
  enabled: true
  path: /
  hosts:
    - host: observability.internal.suse.com

  
