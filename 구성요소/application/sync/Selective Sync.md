---
date: 2024-01-30
tags:
  - argocd
  - sync
  - yaml
aliases: 
category: argocd
links:
  - "[[Sync Option]]"
---
# 정의

기본적으로 Auto Sync를 수행할 때, Application 내에 있는 모든 리소스에 대해서 Sync 작업을 수행한다. 하지만 만약에 Application 내에 있는 리소스 수가 엄청 많은 경우에는 해당 작업이 부하가 될 수있다. 이 경우 Selective Sync를 통해서 Out Of Sync 대상의 리소스만 Sync 작업을 수행할 수 있다.


## 옵션 설정


Selective Sync는 Application Level에서만 지정할 수 있다. 

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: 
  name: auto-selfheal-demo
  namespace: argocd
spec: 
  ...
  syncPolicy:
    syncOptions:
      - ApplyOutOfSyncOnly=false
```
