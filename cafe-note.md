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

Before creating the ExternalDNS kind, create a data center then create a server pointing to the BIG-IP GTM device (Don't forget that the IP must be the self IP, not management IP). After that, update the `dataServerName` in the `edns-*.yaml` to point to the server in GSLB. My case is `/Common/bigip1`. Then create the ExternalDNS:

```
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/cis/cafe/edns-tea.yaml
kubectl create -f k8s-bigip-ctlr/user_guides/externaldns-nginx/cis/cafe/edns-coffee.yaml
```
At this point, CIS should trigger WideIP configuration for GTM.

That's all. Do let me know on any input/correction/suggestion.

Good luck! 
