# EDUC-PROMETHEUS-GRAFANA

Steps for installing Prometheus and Grafana. This installation includes the use of blackbox exporter to allow probes against our containers.  

## What this repository contains
This repository contains OpenShift deployment templates for BlackBox, Prometheus and Grafana. Running the instructions below should stand up an instance of Education monitoring stack. This includes two dashboards which are monitoring Education services (in your namespace). 
* In order to modify targets, modify the `prometheus-application.yaml` file. Specifically, the `prometheus.yml` section
```
static_configs:
 - targets:
   - https://digitalid-api-${NAMESPACE}-dev.pathfinder.gov.bc.ca/health
   - http://grafana-${NAMESPACE}-tools.pathfinder.gov.bc.ca
   - https://pen-demographics-api-${NAMESPACE}-dev.pathfinder.gov.bc.ca/health
   - https://pen-request-api-${NAMESPACE}-dev.pathfinder.gov.bc.ca/health
   - https://pen-request-email-api-${NAMESPACE}-dev.pathfinder.gov.bc.ca/health
...
```
* You will need to create your own dashboards to probe any endpoints your team needs

## BlackBox Exporter Deployment
Black box is used to allow probes between Prometheus and Grafana
* Blackbox can be deployed by cloning this repository locally from Git
* Switch to the correct project/namespace (tools)
* Navigate to the `./blackbox` folder
* Run the following command where the `namespace` value is your namespace and `environment` is the environment you wish to deploy to.

```
oc new-app -f blackbox-application.yaml -p NAMESPACE=<your namespace i.e. v3s4sw> -p ENVIRONMENT=<your env i.e. tools>
```

## Prometheus Deployment
* Prometheus can be deployed by cloning this repository locally from Git
* Switch to the correct project/namespace (tools)
* Navigate to the `./prometheus` folder
* Run the following command where the `namespace` value is your namespace and `environment` is the environment you wish to deploy to.

```
oc new-app -f prometheus-application.yaml -p NAMESPACE=<your namespace i.e. v3s4sw> -p ENVIRONMENT=<your env i.e. tools> 
```

## Grafana Deployment
* Grafana can be deployed by cloning this repository locally from Git 
* Switch to the correct project/namespace (tools)
* Navigate to `./grafana` folder
* Run the following command where the `namespace` value is your namespace and `environment` is the environment you wish to deploy to.
* You can also include the `EMAIL_SUPPORT_LIST` paramater if you wish to receive alerts. List is comma separated. 
* The `PROD_URL` parameter allows you to add a vanity URL if your app contains one (specific to our implementation)

```
oc new-app -f grafana-application-dc.yaml -p NAMESPACE=<your namespace i.e. v3s4sw> -p ENVIRONMENT=<your env i.e. tools> -p EMAIL_SUPPORT_LIST="abc@sda.com,akdl@sadf.com" -p PROD_URL=<your prod URL e.g. vanity URL>
```
