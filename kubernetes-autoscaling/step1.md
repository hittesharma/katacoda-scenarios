# Kubernetes Metric Server
  Metrics Server tells about resource usage data. It collects metrics like CPU or memory consumption for pods.
  - Command 1: Clone K8s Metric Server from GitHub
    
    cd /
    
    git clone https://github.com/kubernetes-incubator/metrics-server.git

## Adding some commands
  - Command 2: 
    
    vim cd /root/metrics-server/deploy/kubernetes/metrics-server-deployment.yaml
  
  This is a manifest yaml file, adding few lines of yaml script to make it work properly. 

    #NEW commands to add starting here ----
    command:
    - /metrics-server
    - --metric-resolution=30s
    - --kubelet-insecure-tls
    - --kubelet-preferred-address-types=InternalIP
    #... ending here
    volumeMounts:
    #some more script code already present in file...
    
## Installation of Metric server
  - Command 3: 
  kubectl apply -f .
  
## Verification of installation 
  - Command 4: 
  kubectl get po -n kube-system |grep metrics

## View metrics information 
  Wait 15 seconds to allow processes to up and hit following command:
  - Command 5: 
  kubectl top pod --all-namespaces
 
