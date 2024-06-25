---
date: 2024-01-30 13:40
tags:
  - argocd
  - sync
  - "#selfhealing"
aliases: 
category: argocd
links:
  - "[[Sync]]"
---
# 정의

ArgoCD에서 Git은 단일 진실 원천(Source Of Truth)이기 때문에 Auto Sync를 활성화하면 Git의 내용을 토대로 k8s 리소스를 관리한다.

하지만 만약 k8s 운영자가 k8s 리소스에 대해 임의로 변경을 가했을 때는 어떻게 해야할까? 이는 의도된 변경일 수도 있고 테스트 용도일 수도 있다.

이 경우 ArgoCD에서는 변경된 사항에 대해서 자동으로 Git의 원래 정의된 속성으로 다시 맞출지 아니면 Sync를 수행하지는 않고 Out Of Sync 상태로 둘지 결정할 수 있으며, 해당 속성이 Self Healing이다.

![[ArgoCD_Sync_SelfHeal.png]]


UI에서는 위와 같이 Sync를 지정할 때 SELF HEAL 체크박스를 통해서 활성화를 수행할 수 있다.



```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: 
  name: auto-selfheal-demo
  namespace: argocd
spec: 
  destination:
    namespace: auto-selfheal-demo
    server: "https://kubernetes.default.svc"
  project: default
  source: 
    path: guestbook-with-sub-directories
    repoURL: "https://github.com/mabusaa/argocd-example-apps.git"
    targetRevision: master
    directory:
      recurse: true
  syncPolicy:
    automated:
      selfHeal: true
    syncOptions:
      - CreateNamespace=true
```

Yaml로 정의하는 경우에는 위와 같이 selfHeal 속성에 true를 지정하여 옵션을 활성화 할 수 있다.