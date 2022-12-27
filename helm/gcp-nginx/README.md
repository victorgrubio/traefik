# GCP Traefik Nginx example

Based on commands from the GCP Cloud Armour setup for traefik available [here](https://traefik.io/blog/protect-applications-with-google-cloud-armor-and-traefik-proxy/)

[Just me and open source playlist](https://www.youtube.com/playlist?list=PL34sAs7_26wNldKrBBY_uagluNKC9cCak)

[Mingshu article](https://minghsu.io/posts/integrate-traefik-with-cloud-ingress/)


Run commands

```bash
helm upgrade --install traefik traefik/traefik -f values-traefik.yaml -n traefik --create-namespace

kubectl create -f ./gcp-nginx/ingress-catch-all.yaml

kubectl create -f ./gcp-nginx/healthcheck.yaml

gcloud compute health-checks list   # Get available healthchecks
gcloud compute health-checks update http --request-path "/healthcheck" HEALTHCHECK_NAME

kubectl create namespace nginx

kubectl create -f ./gcp-nginx/nginx-deploy-main.yaml -f ./gcp-nginx/nginx-deploy-blue.yaml

kubectl create -f ./gcp-nginx/strip-path-middleware-routes.yaml
```