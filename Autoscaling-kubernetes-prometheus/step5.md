To create our deployment, let's use one of k8s example web servers.

First we need to enable the "metrics-server" addon:

`minikube addons enable metrics-server`{{execute}}

Download and deploy the web server

`kubectl apply -f https://k8s.io/examples/application/php-apache.yaml`{{execute}}

After waiting a minute, the dashboard will start receiving some data from the deployment at this time.

Now, we set up the autoscaler:

`kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10`{{execute}}

This command specifies which deployment should be scaled, the target CPU usage, and the maximum and minimum number of replicas.