# Service Registry Application GitOps



## Where is my CI configuration ?

* [components/apicurio-registry/base/.tekton](components/apicurio-registry/base/.tekton) 
* [components/service-api/base/.tekton](components/service-api/base/.tekton)


## Where is my CD configuration ?

* [components/apicurio-registry/base](components/apicurio-registry/base) 
* [components/service-api/base](components/service-api/base)
* [components/sso/base](components/sso/base)

## Try !

After setting up the cluster using https://github.com/sbose78/service-registry-cluster-gitops, create the following to install the application components that would power the Service Registry

```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: service-registry-apps
  namespace: service-registry-staging
spec:
  destination:
    server: 'https://kubernetes.default.svc'
  project: default
  source:
    path: environments/overlays/staging
    repoURL: 'https://github.com/redhat-appstudio-tenants/service-registry-gitops'
    targetRevision: HEAD
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - Validate=false
      - PruneLast=true
```
