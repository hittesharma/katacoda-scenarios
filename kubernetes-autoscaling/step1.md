# Kubernetes Metric Server
  Metrics Server tells about resource usage data. It collects metrics like CPU or memory consumption for pods.
  - Command 1: Clone K8s Metric Server from GitHub
    
    `cd /`{{execute}}<br/>
    
    `git clone https://github.com/kubernetes-incubator/metrics-server.git`{{execute}}

## Adding some commands
  - Command 2: 
    
    `vim metrics-server/deploy/kubernetes/metrics-server-deployment.yaml`{{execute}}
  
  This is a manifest yaml file, adding few lines of yaml script to make it work properly.
    
    ```
     command:
     - /metrics-server
     - --metric-resolution=30s
     - --kubelet-insecure-tls
     - --kubelet-preferred-address-types=InternalIP`
    ```{{copy}}
    
## Installation of Metric server
  - Command 3: 
  `kubectl apply -f .`{{execute}}
  
## Verification of installation 
  - Command 4: 
  `kubectl get po -n kube-system |grep metrics`{{execute}}

## View metrics information 
  Wait 15 seconds to allow processes to up and hit following command:
  - Command 5: 
  `kubectl top pod --all-namespaces`{{execute}}
