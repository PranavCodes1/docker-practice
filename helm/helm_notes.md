# HELM FOR KUBERNETES


HELM - is a package manager for kubernetes, just like we use homebrew/apt/yum to install applications, helm is used to install kubernetes applications.  
it simplifies complicatied application deployments into a single command.

for example- if we want to install prometheus into our k8s cluster for monitoring, prometheus is made up of many different components such as gateways,alert manager etc. so we had to write our own yaml files for pods,deployment,services,secrets, so starting from scratch is a lot of work.  
solution- Helm charts are used to simplify Kubernetes application deployment.

## Helm Charts

Helm Charts- collection of yaml files that are bundled together. helm charts are in public repositories and are available to use.

command for installing the aplication-

```bash
helm install myrelease prom/prometheus
```

Helm charts also provides templating ie it allows customizing the application according to our needs.

# HELM COMPONENTS

there are 3 primary concepts of helm

## 1.Helm Chart

Bundle of YAML files necessary to create k8s application.  
supports helm templating.  
stored in public/private repos.

## 2.Config values

dynamic configuration for customizing deployment of helm charts/ helm releases.  
can be set via CLI arguments or provided in values.yaml file.

## 3.Helm releases

running instance of a helm chart combined with a specific configuratiion.  
it allows us to install,upgrade or rollback any deployments.  
helm chart may have multiple releases such as: dev,test,prod.



# Helm repositories

public and private repositories  
open source helm charts caan be found on artifacts hub.


# HELM TEMPLATING

allows us to customize the heml releases.  
ex- we have a kubernetes application, we will be running multiple instances of this application, such as instance in dev environment, test environment and production environment,so the the requirements and configuration for these environments will be different, so here instead of managing different yaml files for each environment, we will define a common blueprint from helm chart in which dynamic values will be overridden.  
default values will be provided in values.yaml file.


# FOLDER STRUCTURE FOR HELM CHART

```text
webapp1- name of helm chart
|-- chart.yaml (contains metadata such as name ,description,version)
|-- tedmplates
|   |-- NOTES.txt
|   |-- configmap.yaml
|   |-- deployment.yaml
|   |-- service.yaml
|-- values-dev.yaml
|-- values-prod.yaml
|-- values-qa.yaml
|-- values.yaml
```

here values yaml files contains the configuration for the chart. values.yaml is default config values for charts.



# Helm Versions

## helm v2

client/server model.  
depends on "tiller" service, tiller was a additional server to manage the changes to kubernetes.  
uses 'configmaps' as strong driver.  
uses Tiller namespace.  
more dependencies/more complex.

## helm v3

client only,talks directly to kubernetes api.  
uses 'seacrets' as strong driver.  
uses user namespace.  
improved chart upgrade strategies.  
less dependencies/less complex.


# HELM COMMANDS

## 1.helm repo [command]

-used for repository management and listing helm packages

available commands under helm repo-

- add (add a chart repository)
- index (generate an index file given a directory containing pakaged charts)
- list  (list chart repositories)
- remove (remove one or more chart repositories)
- update (update information of available charts locally from chart repositories)


## 2.helm install / uninstall[...]

- install/uninstall a helm chart.

command-

```bash
helm install [name] [chart]
helm uninstall [release name]
```


## 3.helm status [release name]

-gives details of a helm installation: revision,deployment time, current status etc.


## 4.helm list [flags]

- list out helm releases in your environment.


# HELM UPGRADE & ROLLBACK

Helm allows updating applications without redeploying from scratch.

Example:

```bash
helm upgrade monitoring prometheus-community/kube-prometheus-stack -f values.yaml
```

Rollback to previous version:

```bash
helm rollback monitoring 1
```

Benefits:

- safer deployments
- easy recovery
- version management


# helm search repo

coomand-

```bash
helm search repo prometheus
```

Used to search charts from added repositories.  
Very commonly used.
