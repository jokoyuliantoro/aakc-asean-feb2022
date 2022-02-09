# Step-by-Step Setting Up AAKC
This is based on the guide from [Mark Dittmer's guide](https://github.com/mdditt2000/k8s-bigip-ctlr/tree/main/user_guides/externaldns-nginx).

Starting point for this SbS is an Ubuntu 20.04 and a BIG-IP VE with LTM+DNS provisioned. Below is the architecture of my test:

![Test Architecture](aakc-test-architecture.png)

The CIS will be deployed using ClusterIP mode. This requires a VXLAN tunnel 

## BIG-IP Configuration


## Kubernetes Installation
Next step is to install Kubernetes 1.19.x with Flannel. 
