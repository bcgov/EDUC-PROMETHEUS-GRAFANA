# EDUC-PROMETHEUS-GRAFANA

Steps for installing Prometheus and Grafana. This installation includes the use of blackbox exporter to allow probes against our containers.  


oc set volume dc/grafana --add --name=openshift-monitoring-grafana-datasource-volume --type=secret --secret-name=openshift-monitoring-grafana-datasource --mount-path=/etc/grafana/provisioning/datasources --namespace=<namespace>
oc set volume dc/grafana --add --name=grafana-dashboards-config --type=configmap --configmap-name=grafana-dashboards-config --mount-path=/etc/grafana/provisioning/dashboards --namespace=<namespace>
oc set volume dc/grafana --add --name=grafana-predefined-dashboards-config --type=configmap --configmap-name=grafana-predefined-dashboards-config --mount-path=/dashboards --namespace=<namespace>