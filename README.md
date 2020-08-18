# EDUC-PROMETHEUS-GRAFANA

Steps for installing Prometheus and Grafana. This installation includes the use of blackbox exporter to allow probes against our containers.  

## What this repository contains
This repository contains OpenShift deployment templates for BlackBox, Prometheus and Grafana. Running the instructions below should stand up an instance of Education monitoring stack. This includes two dashboards which are monitoring Education services (in your namespace). 
* In order to modify targets, modify the `prometheus-application.yaml` file. Specifically, the `prometheus.yml` section
```
static_configs:
 - targets:
   - https://digitalid-api-${COMMON_NAMESPACE}-${ENVIRONMENT}.pathfinder.gov.bc.ca/health
   - http://grafana-${NAMESPACE}-${ENVIRONMENT}.pathfinder.gov.bc.ca
   - https://pen-demographics-api-${NAMESPACE}-${ENVIRONMENT}.pathfinder.gov.bc.ca/health
   - https://pen-request-api-${NAMESPACE}-${ENVIRONMENT}.pathfinder.gov.bc.ca/health
   - https://pen-request-email-api-${NAMESPACE}-${ENVIRONMENT}.pathfinder.gov.bc.ca/health
...
```
* You will need to create your own dashboards to probe any endpoints your team needs

## BlackBox Exporter Deployment
To Delete existing blackbox switch to namespace where you want to delete, then run the below command.
`oc delete all,rc,svc,dc,route,pvc,secret,configmap,sa,RoleBinding -l name=blackbox`

* Run the following command after replacing the placeholder values. NAMESPACE here is common namespace.

```
oc new-app -f https://raw.githubusercontent.com/bcgov/EDUC-PROMETHEUS-GRAFANA/master/blackbox/blackbox-application.yaml -p NAMESPACE=<your common namespace> -p ENVIRONMENT=<your env i.e. tools> -p DOMAIN =<Domain name goes here.>
```

## Prometheus Deployment
To Delete existing Prometheus switch to namespace where you want to delete, then run the below command.
`oc delete all,rc,svc,dc,route,pvc,secret,configmap,sa,RoleBinding -l name=prometheus`

* Run the following command after replacing the placeholder values.

```
oc new-app -f https://raw.githubusercontent.com/bcgov/EDUC-PROMETHEUS-GRAFANA/master/prometheus/prometheus-application-single-env.yaml -p COMMON_NAMESPACE=<your common namespace> -p PEN_NAMESPACE=<pen namespace i.e. v3s4sw> -p ENVIRONMENT=<your env i.e. tools> 
```

## Grafana Deployment

To Delete existing grafana switch to namespace where you want to delete, then run the below command.
`oc delete all,rc,svc,dc,route,pvc,secret,configmap,sa,RoleBinding -l name=grafana`

* Run the following command after replacing the placeholder values.
* You can also include the `EMAIL_SUPPORT_LIST` parameter if you wish to receive alerts. List is comma separated. 
* The `PROD_URL` parameter allows you to add a vanity URL if your app contains one (specific to our implementation)

```
oc new-app -f https://raw.githubusercontent.com/bcgov/EDUC-PROMETHEUS-GRAFANA/master/grafana/grafana-application-dc.yaml  -p COMMON_NAMESPACE=<your common namespace> -p PEN_NAMESPACE=<pen namespace i.e. v3s4sw> -p ENVIRONMENT=<your env i.e. tools> -p EMAIL_SUPPORT_LIST="abc@sda.com,akdl@sadf.com"
```
