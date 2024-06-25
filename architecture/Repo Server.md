---
date: 2024-01-29 22:51
tags:
  - argocd
  - architecture
  - gitops
aliases: 
category: argocd
links:
  - "[[Architecture]]"
---
# 정의


![[ArgoCD_Repo Server.png]]


Repo Server는 외부에 존재하는 git을 clone하고 필요한 k8s manifest를 생성하는 작업을 수행한다.


# 주요 제공 기능

- Git Repo Clone
- k8s manifest 생성