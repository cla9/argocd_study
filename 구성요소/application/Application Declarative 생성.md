---
date: 2024-01-29 23:20
tags:
  - argocd
  - application
  - gitops
  - "#yaml"
aliases: 
category: argocd
links:
  - "[[Application]]"
---
# 구성 요소


![[ArgoCD_Application_Declarative.png]]


Application은 크게 4가지 영역으로 구성되어있다.

1. K8S Resource Definition 
2. Metadata
3. Cluster 정의
4. Source Manifest 정보


위 영역 중 가장 중요한 것은 바로 Source와 Destination으로 구분된 영역이다.

Source는 Git의 주소와 Repository 내부에서 State가 저장된 path 그리고 targetRevision 등이 지정되어있다.

Desitnation은 App이 배포될 k8s Cluster 및 namespace 등을 지정한다.


```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: 
  name: guestbook
  namespace: argocd
spec: 
  destination: 
    namespace: guestbook
    server: "https://kubernetes.default.svc"
  project: default
  source: 
    path: guestbook
    repoURL: "https://github.com/mabusaa/argocd-example-apps.git"
    targetRevision: master
  syncPolicy:
    syncOptions:
      - CreateNamespace=true
```


기본적인 Application은 위 예시와 같이 지정할 수 있으며, 자세한 내용은 [Application Yaml 옵션](https://argo-cd.readthedocs.io/en/stable/operator-manual/application.yaml)을 참고하자