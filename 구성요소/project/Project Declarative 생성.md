---
date: 2024-01-30 09:00
tags:
  - argocd
  - gitops
  - project
  - "#yaml"
aliases: 
category: argocd
links:
  - "[[Project]]"
---
# 구성 요소


![[ArgoCD_Project_Declarative.png]]


위 Yaml 코드 모습은 Project에서 기본적인 포맷을 나타낸다.


SourceRepo의 경우 해당 Project 내에 있는 Application이 어떠한 Repo가 허용되는지를 의미하는데, * 로 표시된 경우 이는 어떠한 Repo가 포함될 수 있음을 의미한다.

Destination의 경우는 어떠한 Cluster와 Namespace가 위치할 수 있는지를 의미하는데 마찬가지로 위 코드는 모든 Cluster 및 Namespace가 위치할 수 있다. 만약 특정 Cluster의 Endpoint가 적혀있으면, 해당 하위 Application은 다른 Cluster와 매칭될 수 없다.


![[Files/argocd/ArgoCD_Project_Declarative_ClusterResourceWhitelist.png]]

ClusterResourceWhitelist는 Cluster 전역에서 특정 종류의 Resource만 허용하는 것이다. 가령 kind에 위에는 * 로 표시되어있지만, Namespace가 적혀있다면, 해당 Project 내에서 자원 대상은 Namespace로 한정되어진다.


![[Files/argocd/ArgoCD_Project_Declarative_NamespaceResourceWhitelist.png]]

NamespaceResourceWhitelist는 특정 Namespace 영역에서 특정 Resource만 허용하는 것을 의미한다.  가령 위 그림과 같이 Deployment가 표시되어있으면, 해당 namespace에는 Deployment만 사용이 허용된다.

![[ArgoCD_Project_Declarative_NamespaceResourceBlacklist.png]]

NamespaceResource는 Whitelist로 구성할 수도 있지만, Blacklist 방식으로도 처리가 가능하다. 위 예는 NetworkPolicy에 대해서만 거부하고 나머지는 허용하는 것을 의미한다.


![[ArgoCD_Project_Declarative_Role.png]]


Project 내에서는 RBAC을 지정할 수 있다. 여기서는 policy가 사용되는데, 해당 project에 대해서 구체적인 인가 정책을 적용할 수 있다.


다만 Project에서 지정한 role의 경우는 JWT를 생성하지 않고서는 유용하게 적용할 수 없다. JWT는 ArgoCD CLI를 통해서 생성할 수 있는데, 이때 생성된 JWT는 ArgoCD 내부에 저장하지 않는 특징이 있다. 따라서 생성한 JWT는 자체적으로 보관해야한다.

```bash
argocd proj role create-token PROJECT ROLE-NAME
```

Token 생성 기본 CLI 명령어는 위와 같으며, 이를 통해 생성한 Token을 기반으로 CI 시스템에서 해당 Token을 Pass하여 전달할 수 있다. 위 명령어에서 PROJECT는 ArgoCD에서 관리되는 Project 명이며, ROLE-NAME은 Project에 정의된 Role 이름을 의미한다.

```bash
argocd cluster list--auth-token TOKEN
```


위 예는 CLI를 통해  token을 사용한 예시이다. 이때는 --auth-token flag를 통해 token을 전달할 수 있다.

