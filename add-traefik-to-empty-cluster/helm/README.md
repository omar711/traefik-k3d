# Helm assisted Traefik install

Here I've used Helm to generate Traefik installation files.  

I took the template `values.yml` file from https://raw.githubusercontent.com/traefik/traefik-helm-chart/master/traefik/values.yaml and trimmed it down a little.  

Render config using, e.g.:

```
helm template -f values.yml -n kurtosis-engine-08c310fef53441fe87973f33d045b58b --release-name kurtosis traefik/traefik > helm-traefik-template-dummy-render.yaml
```

To install, first apply Traefik CRDs (ref: https://doc.traefik.io/traefik/user-guides/crd-acme/#ingressroute-definition): 

```
# Install Traefik Resource Definitions:
kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.10/docs/content/reference/dynamic-configuration/kubernetes-crd-definition-v1.yml

# Install RBAC for Traefik:
kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.10/docs/content/reference/dynamic-configuration/kubernetes-crd-rbac.yml
```

Then apply your Traefik install:

```
kubectl apply -f helm-traefik-template-dummy-render.yaml
```

