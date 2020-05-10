Make sure our minikube cluster is running:

It starts automatically but it make take a minute to be ready. Be patient :).

`minikube status`{{execute}}

Make sure that the `metrics-server` addon is disabled for now

`minikube addons list`{{execute}}