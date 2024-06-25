---
date: 2024-01-30 12:00
tags:
  - argocd
  - application
  - "#sync"
  - yaml
aliases: 
category: argocd
links:
  - "[[Application]]"
  - "[[Automated Pruning]]"
  - "[[Sync Self Healing]]"
  - "[[Sync Option]]"
---
# Basic


[[기본 컨셉]]에서 ArgoCD는 기본적으로 3분 마다 Git Repo와 적용된 리소스간의 상태를 비교한다고 설명했다.

비교하여 만약 서로 다르면 OutOfSync 상태가 되는데, 이것을 동기화 하기 위해서는 수동으로 Sync를 수행하거나 자동으로 Sync를 수행할 수 있다.

수동으로 수행했을 때는 ArgoCD 에서 Rollback할 수 있는 기능을 제공하지만, 자동으로 Sync를 수행하면 Rollback은 수행할 수 없다.

다만 수동으로 수행하는 것보다 자동으로 수행했을 때에는 CI/CD 파이프라인을 수행하는 과정에서 ArgoCD를 통해서 수동으로 Sync 작업을 진행하지 않아도 되는 장점이 존재한다.

![[ArgoCD_Auto_Sync_UI.png]]


Auto Sync를 수행하는 방법은 CLI 혹은 UI 그리고 Yaml을 통해서 모두 가능하다. 위 예시는 UI에서 Sync Policy를 적용했을 때 모습이다.

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: 
  name: auto-sync-app
  namespace: argocd
spec:
  destination:
    namespace: auto-sync-app
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
```

Yaml을 통해서 Auto로 수행하는 것은 위와 같이 automated: {} flag를 명시하는 것이다.


# 부가 옵션


Auto Sync에는 부가적인 옵션이 존재하는데, 이를 이해하는 것이 무엇보다 중요하다. 이에 대해서 하나씩 알아보자.

## 1. Pruning

![[Automated Pruning]]



# 2. Self Healing

![[Sync Self Healing]]


# 3. 기타 옵션

![[Sync Option]]