first we set up our visualization stack

clone `kube-prometheus` repository

`git clone https://github.com/coreos/kube-prometheus.git`{{execute}}

next, we go into the repository and spawn the monitoring namespaces and containers.

`cd kube-prometheus`{{execute}}

`kubectl create -f manifests/setup`{{execute}}

To check for the status of the monitoring containers use:
`kubectl get pods --namespace=monitoring`{{execute}}

**Be sure to wait each command is completed and all containers are running before moving to the next command**

`kubectl create -f manifests/`{{execute}}

