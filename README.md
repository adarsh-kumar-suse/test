# test



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


helm upgrade --install cert-manager oci://dp.apps.rancher.io/charts/cert-manager -n cert-manager \
--set "global.imagePullSecrets[0].name=application-collection" --set crds.enabled=true
kubectl get pods --namespace cert-manager



# If you have installed the CRDs manually, instead of setting installCRDs or crds.enabled to true in your Helm install command, you should upgrade your CRD resources before upgrading the Helm chart:
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/<VERSION>/cert-manager.crds.yaml

# Add the Jetstack Helm repository
helm repo add jetstack https://charts.jetstack.io

# Update your local Helm chart repository cache
helm repo update

# Install the cert-manager Helm chart
helm install cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --set crds.enabled=true











global:
  imagePullSecrets:
  - application-collection
persistence:
  enabled: true
  storageClass: longhorn
ingress:
  host: rke2c5.demo.com
ollama:
  enabled: true
  defaultModel: llama3.2
  ollama:
    models:
      pull:
      - "llama3.2"
      - "gemma:2b"
extraEnvVars:
- name: VECTOR_DB
  value: "milvus"
- name: MILVUS_URI
  value: "http://milvus.suse-ai.svc.cluster.local:19530"
- name: RAG_EMBEDDING_MODEL
  value: \"sentence-transformers/all-MiniLM-L6-v2[3:36 PM]------------
cat milvus_custom_overrides.yaml
global:
  imagePullSecrets:
  - application-collection
cluster:
  enabled: false
standalone:
  persistence:
    persistentVolumeClaim:
      storageClass: longhorn
etcd:
  replicaCount: 1
  persistence:
    storageClassName: longhorn
minio:
  mode: standalone
  replicas: 1
  rootUser: admin
  rootPassword: adminminio
  persistence:
    size: 100Gi
    storageClass: longhorn
  resources:
    requests:
      memory: 4096Mi
kafka:
  enabled: false
