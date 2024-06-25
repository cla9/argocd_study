---
date: 2024-01-31
tags:
  - argocd
  - github
  - webhook
aliases: 
category:
  - argocd
links:
  - "[[Sync]]"
  - "[[Github App 연계]]"
  - "[[Github Repistiory 등록]]"
---
# 개요


ArgoCD는 기본적으로 3분마다 Git 상태를 비교한다고 [[기본 컨셉#Refresh|기본 컨셉]]에서 설명했다. 즉 Auto Sync를 설정했다고 할지라도 동기화 하려면 최소 3분간은 기다려야 함을 의미한다. 따라서 이를 단축시키기 위해서는 Git에 Push 요청이 왔을 때 ArgoCD에게 Webhook을 전달해서 바로 Sync가 가능하도록 구성하는 것이 좋다.


# 적용 방법


## 1. Repository 이동

먼저 Webhook을 Trigger 하고자하는 k8s yaml 파일이 존재하는 Repository로 접속한다.


## 2. Webhook 메뉴 이동

Repository에서 Settings > Webhooks 메뉴로 이동한다.

![[ArgoCD_Webhook_Menu.png]]

## 3. Webhook 생성


Add webhook 버튼을 클릭하여 Webhook을 생성한다.

![[ArgoCD_Add_Webhook.png]]


## 4. 상세 내용 작성

Payload URL은 ArgoCD의 Webhook URL을 기입해야한다. 기본 값으로 /api/webhook이 Webhook URL로 지정되어있다.

![[ArgoCD_Webhook_Detail.png]]

Secret을 지정하면, Payload URL로 전송된 POST 요청이 Github에서 제공되는 Webhook인지 알 수 있다. 따라서 Secret을 지정하는 것이 좋다. 

상세 내용을 작성하면 Add webhook을 눌러 webhook을 생성한다.


## 5. ArgoCD secret 적용


ArgoCD에서는 argocd-secret 리소스를 통해서 Github에서 생성한 secret을 적용할 수 있다. 자세한 내용은 [ArgoCD 공식 문서](https://argo-cd.readthedocs.io/en/stable/operator-manual/webhook/#2-configure-argo-cd-with-the-webhook-secret-optional)를 참조하자.


### 5.1 Secret 변경


```bash
kubectl edit secret argocd-secret -n argocd
```

Secret 수정을 위해 위 명령어를 입력한다.


### 5.2 Github Secret Key 추가


```yaml
apiVersion: v1
kind: Secret
metadata:
  labels:
    app.kubernetes.io/name: argocd-secret
    app.kubernetes.io/part-of: argocd
  name: argocd-secret
  namespace: argocd
type: Opaque    
data:
  ...
stringData:
  webhook.github.secret : <<Github Secret Key 입력>>  
  
```

위 처럼 secret 값을 입력한 후 저장한다.