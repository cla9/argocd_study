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

ArgoCD 에서 기본적으로 Sync를 진행할 때, 기본적으로 Kubectl을 활용하여 Validation을 진행한다. 이때 몇몇 Resource의 경우에는 이러한 Validation을 사용하지 않을 수도 있다. 따라서 이 경우에는 Disable Kubectl Validation을 활용할 수 있다. Default로는 validation을 수행한다.


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
      - Validate=false
```


Yaml을 통해서 옵션을 설정할 경우에는 위와 같이 Validate 값을 false로 지정하여 설정할 수 있다.


## 2. Resource Level


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    argocd.argoproj.io/sync-options: Validate=false
  name: guestbook-ui
```


Resource 레벨에서 수행한다면, 위와같이 annotation을 이용하여 지정할 수 있다.