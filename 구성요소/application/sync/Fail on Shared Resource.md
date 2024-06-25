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

ArgoCD 에서는 리소스의 Manifest가 여러 Application에서 참조 가능한 형태라도 기본적으로는 Sync 작업을 수행할 때 대상 Application의 리소스에 대해서 apply를 수행한다.

이 경우 여러 Application에서 대상 리소스에 참조할 때 Sync를 실패하게 만드는 옵션으로 FailOnSharedResource가 존재한다.

해당 옵션은 Application Level에서만 적용된다.

# 옵션 설정


```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata: 
  name: auto-selfheal-demo
  namespace: argocd
spec: 
  ...
  syncPolicy:
    syncOptions:
      - FailOnSharedResource=true
```