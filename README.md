# Service Registry Application GitOps



## Where is my CI configuration ?

* [components/apicurio-registry/.tekton](components/apicurio-registry/.tekton) 
* [components/service-api/.tekton](components/service-api/.tekton)


## Where is my CD configuration ?

* [components/apicurio-registry](components/apicurio-registry) 
* [components/service-api](components/service-api)
* [components/sso](components/sso)

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
