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


docker login dp.apps.rancher.io -u adkumar@suse.com -p Z3pweGZ2dHN3Z2RyanZmZG1reGd5YmZmZ3B0aGR2b3RlaXR3d29ydXpubmx1YnFtYm9vY3dmcHNjbHd0emh2Yg==


helm registry login dp.apps.rancher.io -u adkumar@suse.com -p Z3pweGZ2dHN3Z2RyanZmZG1reGd5YmZmZ3B0aGR2b3RlaXR3d29ydXpubmx1YnFtYm9vY3dmcHNjbHd0emh2Yg==



kubectl create secret docker-registry application-collection --docker-server=dp.apps.rancher.io --docker-username=adkumar@suse.com --docker-password=Z3pweGZ2dHN3Z2RyanZmZG1reGd5YmZmZ3B0aGR2b3RlaXR3d29ydXpubmx1YnFtYm9vY3dmcHNjbHd0emh2Yg== -n cert-manager



curl -u adkumar@suse.com:Z3pweGZ2dHN3Z2RyanZmZG1reGd5YmZmZ3B0aGR2b3RlaXR3d29ydXpubmx1YnFtYm9vY3dmcHNjbHd0emh2Yg== https://api.apps.rancher.io/v1/applications
