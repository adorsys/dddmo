# dddmo
drill down data management overview


# Deployment

## Deploymentaccount
We use the namespaced `default` Serviceaccount to create a new kubeconfig for
github actions.

```bash
export SA_TOKEN=default-token-vjx7b
k -n dddmo get secret $SA_TOKEN -o jsonpath='{.data.ca\.crt}' | base64 -d > ca.crt
k config set-cluster dddmo --certificate-authority=ca.crt --embed-certs=true --server=https://z2zn272rbb.adorsys.kaas.cloudpunks.io:31136 --kubeconfig=dddmo.kubeconfig
k config set-credentials dddmo --token=$(k -n dddmo get secret $SA_TOKEN -o jsonpath='{.data.token}' | base64 -d)  --kubeconfig=dddmo.kubeconfig
k config set-context default --current --cluster=dddmo --user=dddmo --kubeconfig=dddmo.kubeconfig
k config use-context default --kubeconfig dddmo.kubeconfig
```
