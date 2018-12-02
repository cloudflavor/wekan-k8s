#### Wekan on kubernetes

Deploying in kubernetes requires an existing mongodb instance running already
in the cluster. The Wekan deployment expects a service named `mongodb` on port
`27017` installed.  
You can install a mongodb instance with [helm](https://helm.sh).

e.g.:

```bash
helm install --name mongodb stable/mongodb --namespace wekan-project --set mongodbRootPassword="pass",mongodbUsername="wekan",mongodbPassword="pass",mongodbDatabase="wekan"
```
The `--name` above will set, among other things, the name of the service that
helm will create. Make sure that name matches the entry in the
[deployment](wekan.yaml) configuration under service.  

Replace the following value with the ones you have in the
deployment file.

```yaml
- name: MONGO_URL
  value: mongodb://wekan:pass@mongodb:27017/wekan
- name: PORT
  value: "8080"
- name: ROOT_URL
  value: http://my.domain.com
```

#### Ingress

Replace

```yaml
  - host: my.domain.com
```
with the proper subdomain name your kubernetes ingress manages.
