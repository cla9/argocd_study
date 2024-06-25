---
date: 2024-01-29 22:44
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


![[ArgoCD_Server.png]]


ArgoCD Server는 Web Server의 역할을 수행한다. 여기에는 화면과 CLI에 의해서 사용되는 API등이 포함된 gRPC 및 Rest API 기능을 제공한다.


# 주요 제공 기능

- Application 관리
- Sync, Rollback
- 인증 , RBAC
- Git Repo 및 Cluster 관리

