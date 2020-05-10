Import our autoscale monitoring dashboard into Grafana:

Download our custom dashboard source to your system:

`https://github.com/javierron/katacoda-scenarios/tree/master/k8s-hpa-visualization/autoscale_monitor.json`

Now, in the Grafana dashboard, press the home button and then in the "import dashboard" button.

Now select the "upload .json" option, and pick the .json file we downloaded previously

Then select your "prometheus" data source and click "Import"

As we have not set up a deployment, the dashboard will receive no data just yet.