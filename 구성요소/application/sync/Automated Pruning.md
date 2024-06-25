---
date: 2024-01-30 13:23
tags:
  - argocd
  - application
  - sync
  - yaml
aliases: 
category: argocd
links:
  - "[[Sync]]"
---
# 정의

Pruning은 말 그대로 가지를 친다는 의미인데, ArgoCD에서 해당 용어는 Git에 정의된 리소스를 삭제 했을 때, k8s 클러스터에 배포되어있는 리소스를 삭제할 것인지를 의미하는 옵션을 의미한다. Default로는 안정성을 위해 Pruning을 수행하지 않는다. 

따라서 해당 옵션을 활성화하면 Git에 리소스가 삭제되었음을 인지하면, k8s에서도 해당 리소스를 삭제한다.


```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: 
  name: auto-pruning-demo
  namespace: argocd
spec: 
  destination:
    namespace: auto-pruning-demo
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
      prune: true
    syncOptions:
      - CreateNamespace=true
```

기본적으로 해당 옵션을 활성화 시키는 방법은 위와 같이 automated 하위에 <font color="#245bdb">prune</font>을 true로 지정하는 것이다.


![[ArgoCD_Auto_Prune_UI.png]]


UI에서 지정할 때는 SYNC Policy 하위에 있는 PRUNE RESOURCES 체크박스를 활성화 시키는 것으로 켤 수 있다.

![[ArgoCD_Manual_Sync_Prune.png]]


지금가지는 Auto Sync에 대해 Prune 설정에 대해 살펴봤지만, Manual Sync를 수행할 때도 Prune을 할 수 있다. 이에 대해서는 [[Manual Snyc Prune]]을 참고하자
