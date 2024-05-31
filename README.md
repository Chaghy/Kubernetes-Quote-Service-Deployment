# Kubernetes-Quote-Service-Deployment

his repository contains the Kubernetes configuration files to deploy a simple quote service application in a development namespace.

Project Overview The project consists of a Kubernetes deployment and service to manage a quote service application. The deployment is configured to run two replicas of the quote-container using the datawire/quote:0.5.0 image and to accept traffic on port 8080.

Files quote.yaml: Kubernetes deployment and service definition file.

Deployment Details Deployment Name: quote-service Namespace: development App Label: quote-service Container Name: quote-container Replicas: 2 Container Image: datawire/quote:0.5.0 Container Port: 8080

Testing with BusyBox To ensure the application can accept traffic from inside the Kubernetes cluster, we use a BusyBox pod for testing.

BusyBox Capabilities BusyBox is a lightweight Unix utility that combines tiny versions of many common UNIX utilities into a single small executable. It provides a minimalist environment, ideal for testing and debugging within Kubernetes clusters.

Testing Steps

Deploy the quote service using the provided quote.yaml file.
Run a BusyBox pod in the same namespace:
kubectl run busybox --image=busybox --restart=Never --namespace=development --rm -it -- /bin/sh

Inside the BusyBox shell, use wget to test the connectivity to the quote service:
wget -qO- http://quote-service:8080
