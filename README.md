# prometheus-grafana

# Monitoring Namespace
We are going to install the monitoring components into a “monitoring” namespace. 

First, create the monitoring namespace:

$ kubectl create -f monitoring-namespace.yaml.

You can now list the namespaces by running

$ kubectl get namespaces

# Prometheus Configuration
Prometheus will get its configuration from a Kubernetes ConfigMap. This allows us to update the configuration separate from the image.

To deploy this to the cluster run

$ kubectl create -f prometheus-config.yaml

You can view this by running

$ kubectl get configmap --namespace=monitoring prometheus-config -o yaml

# Prometheus Pod
We will use a single Prometheus pod for this demo. Take a look at prometheus-deployment.yaml. This is a Kubernetes Deployment that describes the image to use for the pod, resources, etc.

Deploy the deployment by running

$ kubectl create -f prometheus-deployment.yaml

You can see this by running

$ kubectl get deployments --namespace=monitoring

# Prometheus Service
Now that we have Prometheus deployed, we actually want to get to the UI. To do this, we will expose it using a Kubernetes Service
Create the service by running

$ kubectl create -f prometheus-service.yaml

You can then view it by running

$ kubectl get services --namespace=monitoring prometheus -o yaml

# Deploying Grafana
You can deploy grafana by creating its deployment and service by running

$ kubectl create -f grafana-deployment.yaml

and

$ kubectl create -f grafana-service.yaml.

You can then view it by running

$ kubectl get services --namespace=monitoring grafana -o yaml

For the URL, we will actual use Kubernetes DNS service discovery. So, just enter http://<IP>:9191
  
Create a New dashboard by clicking on the upper-left icon and selecting Dashboard->New.

Download the dashboard file from Grafana website https://grafana.com/dashboards/2115 and import it to dashboards.
