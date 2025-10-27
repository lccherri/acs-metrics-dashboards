# ACS Metrics Dashboards

## Pre Requirements

## Configuring Grafana

```bash
# Set the namespace for Grafana deployment
export NAMESPACE=test-gf

# Create the namespace if it doesn't exist
oc create namespace ${NAMESPACE}

# Create a service account named 'monitoring' in the namespace
oc create sa monitoring -n ${NAMESPACE}

# Grant the service account permissions to view cluster monitoring resources
oc adm policy add-cluster-role-to-user cluster-monitoring-view -z monitoring -n ${NAMESPACE}

# Apply the secret for Grafana service account token
oc apply -f ./01-grafana/01-grafana-sa-token-secret.yaml -n ${NAMESPACE}

# Apply the Grafana deployment manifest
oc apply -f ./01-grafana/02-grafana.yaml -n ${NAMESPACE}
oc apply -f ./01-grafana/03-datasource.yaml -n ${NAMESPACE}
```

## Configuring Dashboads

```bash
# Set the namespace for of Grafana
export NAMESPACE=test-gf

oc apply -f ./02-dashboards -n ${NAMESPACE}
```

## Integrate Grafana Login