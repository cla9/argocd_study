---
date: 2024-01-30 11:31
tags:
  - argocd
  - application
  - gitops
  - "#gittracking"
aliases: 
category: argocd
links:
  - "[[Application]]"
---
# 기본 전략


![[ArgoCD_Git_Tracking.png]]


Git Tracking 설정은 [[Application Declarative 생성]]에서 targetRevision 지정 부분에 사용될 수 있다. 혹은 UI를 통해서 Application을 생성할 때도 지정할 수 있다. ArgoCD의 Git Repo Tracking 전략은 위와 같이 4가지다. 

1. Commit SHA 방식으로 Commit 번호 추적
2. Git에서 생성한 Tag 추적
3. Branch 지정하여 해당 Branch에 변화 추적
4. HEAD와 같은 Symbloic reference 추적

Git 외에도 Helm Chat를 추적하는 방식도 존재하나, 여기서는 다루지 않는다.