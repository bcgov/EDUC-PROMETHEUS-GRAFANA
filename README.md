# EDUC-PROMETHEUS-GRAFANA

Steps for installing Prometheus and Grafana. This installation includes the use of blackbox exporter to allow probes against our containers.  

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

```
oc new-app -f grafana-application-dc.yaml -p NAMESPACE=<your namespace i.e. v3s4sw> -p ENVIRONMENT=<your env i.e. tools>
```
