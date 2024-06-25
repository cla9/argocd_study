---
date: 2024-01-30 11:47
tags:
  - argocd
  - application
  - "#diffing"
  - "#customization"
  - yaml
aliases: 
category: argocd
links:
  - "[[Application]]"
---
# Diffing Customization이란

ArgoCD에서는 Git의 Desired State와 K8s에 배포된 리소스의 상태를 비교(Diffing)하여 State를 동기화한다고 [[기본 컨셉#State]]에서 설명했다. 


![[Kubernetes-인증-과정]]


이때 만약 istio와 같은 솔루션을 사용하거나 별도 Mutating Webhook을 적용한다면, 실제 k8s에 적용된 리소스와 Git에 명시된 Yaml Spec이 다를 수 있다. 따라서 이때는 만약 k8s에 적용된 추가된 속성이 있을 지라도 운영상 문제가 없을 경우에는 Customization을 통해서 이를 예외처리할 수 있다.


# Ignoring differences options


ArgoCD에서는 상태가 다른 두 Spec에 대해서 ignoring을 지원하기 위해 3가지 옵션을 제공한다.

1. JSON path
2. JQ path expression
3. metadata.managedFields


```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: 
  name: diffing-customization-demo
  namespace: argocd
spec: 
  destination:
    namespace: diffing-customization-demo
    server: "https://kubernetes.default.svc"
  project: default
  source: 
    path: guestbook-with-sub-directories
    repoURL: "https://github.com/mabusaa/argocd-example-apps.git"
    targetRevision: master
    directory:
      recurse: true
  syncPolicy:
    automated: {}
    syncOptions:
      - CreateNamespace=true
  ignoreDifferences:
    - group: apps
      kind: Deployment
      jsonPointers:
      - /spec/replicas
```

가령 위와 같은 코드가 있을 때 ignoreDifferences 설정에서 jsonPointer로 위치를 지정해주면, 해당 리소스에 path 속성이 다를 지라도 이를 무시한다.


```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: 
  name: istiod
  namespace: argocd
spec: 
  destination:
    namespace: istio-system
    server: "https://kubernetes.default.svc"
  project: default
  source:
    repoURL: 'https://istio-release.storage.googleapis.com/charts'
    targetRevision: 1.13.4
    chart: istiod
  syncPolicy:
    automated: {}
    syncOptions:
      - CreateNamespace=true
  ignoreDifferences:
    - group: admissionregistration.k8s.io
      kind: MutatingWebhookConfiguration
      jqPathExpressions:
        - '.webhooks[]?.clientConfig.caBundle'
```

위 예는 jsonpointer가 아닌 jqPathExpressions를 사용해서 ignore를 적용한 모습이다.