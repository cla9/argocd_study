---
date: 2024-01-31
tags:
  - argocd
aliases: 
category:
  - argocd
links:
  - "[[Access Token 생성]]"
---
# 1. Access Token 생성

[[Access Token 생성]] 내용을 참고하여 Github과 연계할 계정에 대해 Token을 발행한다.

# 2. Repo 등록


## 2-1. Repository 탭 이동

Repository 등록을 위해 Web UI 상의 Settings > Repositories로 이동한다.


![[ArgoCD_Repository.png]]


## 2-2.  Repository 등록

CONNECT REPO 버튼을 클릭 후 Repository 정보를 등록한다.


![[ArgoCD_Repo_Detail.png]]


1. connection method : VIA HTTPS
2. Type : git
3. Repository URL : k8s yaml 배포할 github의 repository 주소
4. Username : 개인 계정
5. Password : 발급받은 Token 

입력 후 Connect 하여 이상 없으면 SAVE AS CREDENTIALS TEMPLATE 버튼을 눌러 등록을 완료한다.
