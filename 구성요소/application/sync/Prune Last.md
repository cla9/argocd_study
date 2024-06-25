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
  - "[[No Prune]]"
  - "[[Automated Pruning]]"
  - "[[Wave]]"
---
# 정의


리소스 삭제가 발생할 때 가장 마지막에 있는 대상으로만 Prune이 필요할 때 사용되는 옵션이다. 이러한 과정은 [[Wave]]에서 설명 되어있듯이 Application 생성/삭제에 순서가 존재하는 경우 마지막 Application 혹은 특정 리소스에 대해서만 선택적으로 삭제가 가능하다.


# 옵션 설정


## 1. Application Level

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
      - PrunLast=false
```


Application Level에서는 위와 같이 PrunLast 옵션에 값을 지정함으로써 활성화가 가능하다.


## 2. Resource Level



```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    argocd.argoproj.io/sync-options: PrunLast=false
  name: guestbook-ui
```


Resource 레벨에서 수행한다면, 위와같이 annotation을 이용하여 지정할 수 있다.