# Nginx Ingress

## Install

```kubectl create ns nginx-ingress```
```
helm install   nginx-ingress stable/nginx-ingress --namespace nginx-ingress  \
--set rbac.create=true \
--set controller.service.type=LoadBalancer \
--set controller.metrics.enabled=true \
--set controller.stats.enabled=true 
```
### Get the public ip address

```
$(kubectl --namespace nginx-ingress get services -o jsonpath="{.status.loadBalancer.ingress[0].ip}" nginx-ingress-controller)
```
 

### Example Ingress Resource

```
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    annotations:
      kubernetes.io/ingress.class: nginx
    name: example
    namespace: foo
  spec:
    rules:
      - host: www.example.com
        http:
          paths:
            - backend:
                serviceName: exampleService
                servicePort: 80
              path: /
    # This section is only required if TLS is to be enabled for the Ingress
    tls:
        - hosts:
            - www.example.com
          secretName: example-tls
```
##### If TLS is enabled for the Ingress, a Secret containing the certificate and key must also be provided:
```
  apiVersion: v1
  kind: Secret
  metadata:
    name: example-tls
    namespace: foo
  data:
    tls.crt: <base64 encoded cert>
    tls.key: <base64 encoded key>
  type: kubernetes.io/tls
```

### HELM 3

helm repo add nginx-stable https://helm.nginx.com/stable
helm repo update

kubectl create ns nginx-ingress

helm install   nginx-ingress stable/nginx-ingress --namespace nginx-ingress  \
--set rbac.create=true \
--set controller.service.type=LoadBalancer \
--set controller.metrics.enabled=true \
--set controller.stats.enabled=true 

helm list -n nginx-ingress

kubectl get svc -n nginx-ingress
