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
  - "[[Automated Pruning]]"
---
# 정의


기본적으로 ArgoCD는 k8s와 Git의 상태를 비교하고 동일하지 않으면, Out Of Sync가 된다고 설명했다. 이럴 경우 [[Diffing Customization]] 방법을 통해서 아예 비교 자체를 수행하지 않도록 특별 path를 지정하는 방법도 있지만, No Prune을 통해서 특정 Resource에 대해서만 Prune을 수행하지 않도록 할 수 있다.

이때 Diffing 방법과 No Prune의 차이는 No Prune을 지정하여도 Out Of Sync 상태는 유지된다.


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    argocd.argoproj.io/sync-options: Prune=false
  name: guestbook-ui
```


설정하는 방법은 위와 같이 개별 리소스 Yaml에 annotation을 추가하여 Prune되지 않도록 지정할 수 있다.

![[ArgoCD_No_Prune.png]]

이 경우 Git에서 해당 리소스를 삭제해도 ArgoCD에서는 해당 리소스를 삭제하지 않는다. 그리고 ArgoCD UI에서는 해당 리소스가 삭제되지 않고 ignored 되었음을 확인할 수 있다.

이때 다시 Sync 상태로 유지하려면, 사용자가 직접 해당 리소스를 삭제하여 Git의 상태와 동기화 시켜야된다.