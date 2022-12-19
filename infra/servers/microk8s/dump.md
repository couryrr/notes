# Kubernetes via microk8s

## Got a cluster!

So far I have 6 laptop - 4 cores each - 8 gb mem each - 250 ssd

Install was pretty easy. Running microk8s for kubernetes.

Adding them to the cluster was strightforward enough. Ran into one hiccup when the ip addressed changed on one of the node before adding static. It breaks selfsigned certs. So nothing could connect.

There did not seem to be a great way to fix it so I removed the snap on all the hosts and re-added them.

## Networking is kicking my ass

I have MetalLB running to hand out ips. It is configured to hand out an ip that my local network should know.

nginx-ingress-controller is being used and it is using the ip address that I expect for external.

I cannot ping that ip-address and cannot hit the service running behind it :(

This is where my networking chops are starting to fail. I know it has to do with the interfaces that are actually listening and how to point traffic from outside to inside. I just have no idea how to do that.
