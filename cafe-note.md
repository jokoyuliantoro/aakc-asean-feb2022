# Cafe Installation Note

The earlier note is available [here](nginx-ic-note.md).

The note is based on Mark Dittmer's guide available [here](https://github.com/mdditt2000/k8s-bigip-ctlr/tree/main/user_guides/externaldns-nginx).

The Cafe installation is the last step and also straightforward.

```
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/ingress-example/cafe.yaml
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/ingress-example/cafe-secret.yaml
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/ingress-example/cafe-ingress.yaml
```

(Optional) If you want to see the CIS in action, tail the log of CIS pod (either using `k logs -f` or `k9s`).

Then create the VS:

```
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/cis/cafe/reencrypt-tls.yaml
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/cis/cafe/vs-tea.yaml
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/cis/cafe/vs-coffee.yaml
```

At this point, CIS should trigger new VS configuration for LTM.

```
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/cis/cafe/edns-tea.yaml
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/cis/cafe/edns-coffee.yaml
```

