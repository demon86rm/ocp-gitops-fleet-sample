# ocp-gitops-fleet-sample

Sample application for the multi-cluster GitOps workshop (Argo CD Agent, ApplicationSet).
It is public on purpose: Argo CD needs no credentials to read it.

One tiny web page, packaged two ways, with a `test` and a `prod` flavour of each:

| Path | Tool | Flavours |
| --- | --- | --- |
| `apps/hello/helm` | Helm chart | `values-test.yaml`, `values-prod.yaml` |
| `apps/hello/kustomize` | Kustomize | `overlays/test`, `overlays/prod` |

The image is `registry.access.redhat.com/ubi9/httpd-24`, which listens on port 8080 and runs under the OpenShift `restricted` SCC. There is no `LoadBalancer` Service. The page is reached through an OpenShift `Route`.

Preview locally:

```bash
helm template hello apps/hello/helm -f apps/hello/helm/values-prod.yaml
oc kustomize apps/hello/kustomize/overlays/prod
```
