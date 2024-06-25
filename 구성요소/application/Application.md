---
date: 2024-01-29 22:25
tags:
  - argocd
  - application
  - concept
  - gitops
aliases: 
category: argocd
links:
  - "[[기본 컨셉]]"
  - "[[Application Declarative 생성]]"
---
# 1. 개념


![[ArgoCD_Application.png]]


Application은 특정 모듈을 이루는 k8s 자원들의 그룹을 의미한다. 즉 하나의 모듈 내에는 Service, Deployment, Ingress 등 여러 요소가 존재하는데, 이러한 자원의 그룹을 ArgoCD 에서는 Application 이라고 부른다.


# 2. 종류

Application은 다양한 형태의 소스를 지원하는데 크게 3가지 종류가 있다.

1. Helm Chart
2. Kustomize 
3. Yaml files 목록 디렉토리


# 3. 주요 정보

- Source : Git에 존재하는 Desired State를 가르킨다.
	- revision
	- path
- Destination : Target Cluster와 Namespace를 가르킨다.


# 4. 생성 방법
1. Yaml 
2. Web UI
3. CLI


위 세 가지 방법 중에서 가장 추천하는 것은 [[Application Declarative 생성|Yaml을 통한 Application 생성]]이다. ArgoCD 의 자원 또한 gitops로 관리될 수 있기 때문에 Yaml로 작성하고 별도의 git에 보관할 수 있는 장점이 있다. 만약 Yaml 작성이 힘들다면, Web UI로 Application을 생성하되, 생성된 결과 또한 ArgoCD의 CRD로 관리되므로 이를 Yaml로 내려받아 git에 보관해도 무방하다.