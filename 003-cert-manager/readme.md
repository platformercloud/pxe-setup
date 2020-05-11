## Cert Manager

### Install

Edit the <EMAIL> at cluster-issuer.yaml to your email

```
kubectl create namespace cert-manager
kubectl label namespace cert-manager certmanager.k8s.io/disable-validation=true
```
``` 
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v0.14.0/cert-manager.yaml 
```
### Delete

``` kubectl delete -f https://github.com/jetstack/cert-manager/releases/download/v0.10.0/cert-manager.yaml```

#### Remove the CRDs:
```
 kubectl delete crd \
    certificates.certmanager.k8s.io \
    issuers.certmanager.k8s.io \
    clusterissuers.certmanager.k8s.io
```