---
date: 2024-01-29 22:57
tags:
  - argocd
  - architecture
  - gitops
aliases: 
category: argocd
links:
  - "[[Architecture]]"
  - "[[ApplicationSet]]"
---
# 정의

![[ArgoCD_ApplicationController.png]]


Application Controller는 실질적으로 State를 비교하기 위한 기능을 제공하는 주요 컴포넌트이다. 주기적으로 k8s에서 동작하는 application과 git에 존재하는 manifest 정보를 비교한다.

# 주요 제공 기능

- Watch 메커니즘을 통해 k8s 자원 상태 확인
- Repo Server를 통해 Git 상태 동기화
- 클러스터에 Sync 작업 수행
- State 비교를 통한 Out of Sync 여부 확인
- Hook을 통한 각 단계 Custom Hook 수행
