Now, we generate some load towards the web server.

Start a new terminal and run the load generator:

`kubectl run -it --rm load-generator --image=busybox /bin/sh`{{execute}}

After it starts we set it on a loop to continously send traffic to our server:

`while true; do wget -q -O- http://php-apache; done`{{execute}}

Now, we wait about 2-3 minutes and see the information being displayed in the Grafana dashboard. Make sure to keep some acitvity in the Katacoda terminal, or it will automatically shut-down.

If then, we stop the load generator, we should be able to observe the dashboard react to that as well.