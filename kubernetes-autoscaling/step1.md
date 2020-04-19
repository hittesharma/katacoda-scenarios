# Kubernetes Metric Server
  Metrics Server tells about resource usage data. It collects metrics like CPU or memory consumption for pods.
  - Command 1: Clone K8s Metric Server from GitHub
    
    `cd /`{{execute}}<br/>
    
    `git clone https://github.com/kubernetes-incubator/metrics-server.git`{{execute}}

## Adding some parameters
  - Command 2: 
    
    `vim metrics-server/deploy/kubernetes/metrics-server-deployment.yaml`{{execute}}
  
  This is a manifest yaml file, adding few lines of yaml script to make it work properly.
    
    ```
            command:
            - /metrics-server
            - --metric-resolution=30s
            - --kubelet-insecure-tls
            - --kubelet-preferred-address-types=InternalIP
    ```{{copy}}
    
## Installation of Metric server
  - Command 3: 
  `kubectl apply -f metrics-server/deploy/kubernetes/`{{execute}}

## View metrics information 
  Wait 20 seconds to allow processes to come up and hit following command:
  - Command 4: 
  `kubectl top pod --all-namespaces`{{execute}}
  
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
   `kubectl autoscale deployment hpa-demo-web --cpu-percent=5 --min=1 --max=5`
   
### 

kubectl get hpa

`kubectl get pod | grep hpa-demo-web`

