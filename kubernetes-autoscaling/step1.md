# Kubernetes Metrics Server</br></br>

## Cloning the metrics server configuration
  - Command 1 :
  `git clone https://github.com/hittesharma/katacoda-scenarios.git`{{execute}}
    
## Installation of Metrics server
  - Command 2: 
  `kubectl apply -f /root/katacoda-scenarios/kubernetes-autoscaling/components.yaml`{{execute}}

## View metrics information 
  Wait 20 seconds to allow processes to come up and hit following command:
  - Command 3: 
  `kubectl get po -n kube-system |grep metrics`{{execute}}
  
## Verify metrics server is running desired number of pods
  - Command 4:
  `kubectl get deployment metrics-server -n kube-system`{{execute}}

---------------------
  
# Installation of Web App & overloading it
In this we will setup a pod that this actually a web server app which prints word 'OK!' upon request.

## Installation of WebApp

### Create deployment 
It will pull the web application image from GCP.
  - Command 5: 
  `kubectl run hpa-demo-web --image=k8s.gcr.io/hpa-example --requests=cpu=200m --port=80 --replicas=1`{{execute}}

### Verification of running pod 
  - Command 6: 
  `kubectl get pod | grep hpa-demo-web`{{execute}}
  
### Start the service
  - Command 7: 
  	`kubectl expose deployment hpa-demo-web --type=NodePort`{{execute}}

### Verification of running service
  - Command 8: 
    `kubectl get service | grep hpa-demo-web`{{execute}}

## Overloading the webapp
Running a loop in the test container that continuously calls hpa-demo-web service

### IN NEW TERMINAL WINDOW, create a test container deployment
  - Command 9: 
  `kubectl run -it deployment-for-testing --image=busybox /bin/sh`{{execute}}

### Verification of running nginx service
  - Command 10:
  `wget -q -O- http://hpa-demo-web.default.svc.cluster.local`{{execute}}

### Creating traffic
  - Command 11:
  `echo "while true; do wget -q -O- http://hpa-demo-web.default.svc.cluster.local ; done" > loops.sh | chmod +x loops.sh | sh       loops.sh`{{execute}}

Don't close the terminal, let the traffic flow. If you wish then you could run this in background using &

-----------------------------------
## Setting up pod auto-scaling

### Listing pods running on high CPU utilization
Go back to the previous terminal where pod named hpa-demo-web was running. Following command requests metrics server.
  - Command 12:
  `kubectl top pods --all-namespaces`{{execute}}
  
### Configuring pod auto-scaling (horizontal) for our deployment 
   - Command 13:
   `kubectl autoscale deployment hpa-demo-web --cpu-percent=5 --min=1 --max=5`{{execute}}
   
### Creating more pods to spread the load, run this command in the interval of 30 seconds to view the difference
   - Command 14: 
   `kubectl get hpa`{{execute}}

### Observe pod creation as per demand 
   - Command 15:
   `kubectl get pod | grep hpa-demo-web`{{execute}}
