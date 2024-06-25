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


기본적으로 ArgoCD 에서 배포를 진행할 때는 kubectl apply 명령어를 이용한다. 하지만 만약 apply가 아니라 replace를 원할 경우 해당 옵션을 사용할 수 있다.


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
      - Replace=true
```


Application Level에서는 Replace 옵션을 통해서 위와 같이 지정할 수 있다.

## 2. Resource Level

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    argocd.argoproj.io/sync-options: Replace=true
  name: guestbook-ui
```


Resource 레벨에서 수행한다면, 위와같이 annotation을 이용하여 지정할 수 있다.