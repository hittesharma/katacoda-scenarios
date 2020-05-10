Now we expose the monitoing services using the `kubectl port-forward` command

Prometheus:

`kubectl --namespace monitoring port-forward --address [[HOST_IP]] svc/prometheus-k8s 9090 &`{{execute}}

Grafana:

`kubectl --namespace monitoring port-forward --address [[HOST_IP]] svc/grafana 3000 &`{{execute}}


The dashboards should now be accessible through the browser.

Prometheus:

https://[[HOST_SUBDOMAIN]]-9090-[[KATACODA_HOST]].environments.katacoda.com/

Grafana:

https://[[HOST_SUBDOMAIN]]-3000-[[KATACODA_HOST]].environments.katacoda.com/

The user/password for the Grafana dashboard is admin/admin by default.

