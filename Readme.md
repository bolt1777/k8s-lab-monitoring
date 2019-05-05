# Vagrant Minikube Lab

## Web UIs

- Grafana: [https://k8s-minikub](https://k8s-minikub)
- Prometheus-UI: [http://k8s-minikub:30900](http://k8s-minikub:30900)

## Installation

```bash
git clone https://github.com/dmarych/k8s-lab-monitoring.git
cd k8s-lab-monitoring
vagrant plugin install vagrant-hostmanager
vagrant up
```

## Grafana

To access Grafana dashboard, use admin/admin login credentials.

# Ansible Role Setup

+ The role **minikube**:
	- Deploys Minikube cluster which responds to Kubernetes API requests

+ The role **monitoring** brings manifests to do the following tasks:
	- Run Prometheus Operator (https://github.com/coreos/prometheus-operator)
	- Deploy kube-state-metrics (https://github.com/kubernetes/kube-state-metrics)
	- Deploy Ingress Nginx in cluster (https://github.com/kubernetes/ingress-nginx)
	- Create Prometheus instance 
	- Add Prometheus scrape job (via Kubernetes CRD created by Prometheus Operator) for kube-state-metrics
	- Deploy Grafana 
	- Add dashboard for kube-state-metrics
	- Expose Grafana via ingress

## Vagrant usage

To log on to Minikube cluster, use vagrant ssh

``
vagrant ssh k8s-minikub
``

## Note:
	- There are some timeouts setup, especially the one which waits while Grafana is deployed and running, it's 300 seconds and then ansible loads dashboard and data source. Please be patient and if anything goes wrong, load the dashboard from the doc folder and add Prometheus to data source http://prometheus:9090
