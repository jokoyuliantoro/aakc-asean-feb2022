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

At this point, CIS should trigger new VS configuration for LTM. Have a look into the right BIG-IP partition which is `k8s` in my case. If you familiarised with the CIS deployment parameters then you know where the partition name is defined.

```
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/cis/cafe/edns-tea.yaml
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/cis/cafe/edns-coffee.yaml
```
At this point, CIS should trigger WideIP configuration for GTM.

That's all. Do let me know on any input/correction/suggestion.

Good luck! 
