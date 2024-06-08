# cloudflare-docker-proxy

![deploy](https://github.com/Mai-Ooizumi/cloudflare-docker-proxy/actions/workflows/deploy.yaml/badge.svg)

> If you're looking for proxy for helm, maybe you can try [cloudflare-helm-proxy](https://github.com/ciiiii/cloudflare-helm-proxy).

## Deploy

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/Mai-Ooizumi/cloudflare-docker-proxy)

1. fork this project
2. modify the link of the above button to your fork url
3. click the button, you will be redirected to the deploy page

## Config tutorial

1. use cloudflare worker host: only support proxy one registry

   ```javascript
   const routes = {
     "${workername}.${username}.workers.dev/": "https://registry-1.docker.io",
   };
   ```

2. use custom domain: support proxy multiple registries route by host
   - host your domain DNS on cloudflare
   - add `CNAME` record of xxx.your.domain to `${workername}.${username}.workers.dev`
   - deploy this project to cloudflare workers
   - add `xxx.your.domain/*` to HTTP routes of workers
   - add more records and modify the config as you need

   ```javascript
   const routes = {
     "docker.your.domain": "https://registry-1.docker.io",
     "quay.your.domain": "https://quay.io",
     "gcr.your.domain": "https://k8s.gcr.io",
     "k8s-gcr.your.domain": "https://k8s.gcr.io",
     "ghcr.your.domain": "https://ghcr.io",
   };
   ```
