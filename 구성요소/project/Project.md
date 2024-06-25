---
date: 2024-01-29 22:29
tags:
  - argocd
  - concept
  - project
  - gitops
aliases: 
category: argocd
links:
  - "[[기본 컨셉]]"
  - "[[Project Declarative 생성]]"
---
# 1. 개념


![[ArgoCD_Project.png]]


Project는 ArgoCD에서 관리하는 Application 들의 logical 한 그룹을 의미한다. 이러한 Project는 ArgoCD를 활용하여 여러 Team에서 다양한 Application을 배포할 때 상호간의 RBAC 정책 등을 적용할 때 사용될 수 있다.


# 2. 사용 용도

1. git repo를 특정한 자원들에게만 적용하고 싶을 경우
2. 특정 Application들을 지정된 clusters와 namespace에 배포하고 싶을 경우
3. application 자원들에 대한 배포 권한을 부여하고 싶을 경우
4. 특정 CI System에 대해서 Application들에 대한 접근 권한을 차등하고 싶을 경우 JWT 같은 것을 활용하여 인증처리할 수 있음


# 3. 특징

Project는 ArgoCD를 설치하면 기본적으로 모든 Application은 Default Project에 속한다.



# 4. 생성 방법

1. Yaml 
2. Web UI
3. CLI


[[Application#4. 생성 방법]] 과 마찬가지로 [[Project Declarative 생성|Yaml을 통한 생성]]을 가장 추천한다. 

