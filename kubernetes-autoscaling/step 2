# Installation of Web App & overloading it
In this we will setup a pod that this actually a web server app which prints word 'OK!' upon request.

## Installation of WebApp

### Create deployment 
It will pull the web application image from GCP.
Command 1: 
  `kubectl run hpa-demo-web --image=k8s.gcr.io/hpa-example --requests=cpu=200m --port=80 --replicas=1`{{execute}}

### Verification of running pod 
Command 2: 
  `kubectl get pod | grep hpa-demo-web`{{execute}}
  
### Start the service
Command 4: 
  	`kubectl expose deployment hpa-demo-web --type=NodePort`{{execute}}

### Verification of running service
Command 5: 
`kubectl expose deployment hpa-demo-web --type=NodePort`{{execute}}

## Overloading the webapp
Running a loop in the test container that continuously calls hpa-demo-web service

### IN NEW TERMINAL WINDOW, create a test container deployment
Command 6: 
`kubectl run -it deployment-for-testing --image=busybox /bin/sh`{{execute}}

### Verification of running nginx service
Command 7:
`wget -q -O- http://hpa-demo-web.default.svc.cluster.local`{{execute}}

### Creating traffic
echo "while true; do wget -q -O- http://hpa-demo-web.default.svc.cluster.local ; done" > loops.sh | chmod +x loops.sh | sh loops.sh

#### Giving executable permission
chmod +x /loops.sh

#### ...if above command doest work
