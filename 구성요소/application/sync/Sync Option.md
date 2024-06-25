---
date: 2024-01-30 13:48
tags:
  - argocd
  - sync
aliases: 
category: argocd
links:
  - "[[Sync]]"
  - "[[No Prune]]"
  - "[[Disable Kubectl Validation]]"
  - "[[Selective Sync]]"
  - "[[Prune Last]]"
  - "[[Replace Resources]]"
  - "[[Fail on Shared Resource]]"
---
# Sync Option

Sync에는 많은 옵션이 존재한다. 이러한 옵션은 대부분 Application을 생성할 때 Application 레벨에서 정의할 수 있다. 혹은 몇몇 옵션의 경우에는 Yaml을 통해 생성할 때 annotation을 지정해서 추가할 수 있다.


```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: 
  name: auto-sync-app
  namespace: argocd
spec:
  ...
  syncPolicy:
    syncOptions:
  ...      
```


이번 장에서는 ArgoCD에서 Sync에 제공되는 Option 기능에 대해서 알아보자.


## 1. No Prune

![[No Prune]]


## 2. Disable Kubectl Validation

![[Disable Kubectl Validation]]


## 3. Selective Sync

![[Selective Sync]]


## 4. Prune Last

![[Prune Last]]


## 5. Replace Resources

![[Replace Resources]]


## 6. Fail on Shared Resource