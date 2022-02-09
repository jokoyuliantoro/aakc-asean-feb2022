# NGINX Ingress Controller Installation Note

The earlier note is available [here](ipam-note.md).

The note is based on Mark Dittmer's guide available [here](https://github.com/mdditt2000/k8s-bigip-ctlr/tree/main/user_guides/externaldns-nginx).

The NGINX IC installation is straightforward. I just followed the guide. But before that, I install the CRD first based on [NGINX IC installation guide](https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/).

```
git clone https://github.com/nginxinc/kubernetes-ingress/
cd kubernetes-ingress/deployments
kubectl apply -f common/crds/k8s.nginx.org_virtualservers.yaml
kubectl apply -f common/crds/k8s.nginx.org_virtualserverroutes.yaml
kubectl apply -f common/crds/k8s.nginx.org_transportservers.yaml
kubectl apply -f common/crds/k8s.nginx.org_policies.yaml
cd ../..
```

Then following the guide:
```
kubectl apply -f k8s-bigip-ctlr/user_guides/externaldns-nginx/nginx-config/ns-and-sa.yaml
kubectl apply -f k8s-bigip-ctlr/user_guides/externaldns-nginx/nginx-config/rbac.yaml
kubectl apply -f k8s-bigip-ctlr/user_guides/externaldns-nginx/nginx-config/default-server-secret.yaml
kubectl apply -f k8s-bigip-ctlr/user_guides/externaldns-nginx/nginx-config/nginx-config.yaml
kubectl apply -f k8s-bigip-ctlr/user_guides/externaldns-nginx/nginx-config/ingress-class.yaml
kubectl apply -f k8s-bigip-ctlr/user_guides/externaldns-nginx/nginx-config/nginx-ingress.yaml
kubectl apply -f k8s-bigip-ctlr/user_guides/externaldns-nginx/nginx-config/nginx-service.yaml
```

Ensure it is running without error message:

=== insert picture ===

Next is installing Cafe in [here](cafe-note.md).
