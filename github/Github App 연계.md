---
date: 2024-01-31
tags:
  - argocd
  - github
  - repository
aliases: 
category:
  - argocd
links:
  - "[[Github App 연계]]"
---
# 1. Github App 생성

[[Organization Github App 생성]]을 참고하여 Github App을 생성한다.

이때 Permission 설정 시 Repositiory Permission은 최소한 [Contents 항목 Read-Only 권한이 지정](https://github.com/argoproj/argo-cd/blob/master/docs/user-guide/private-repositories.md#github-app-credential)되어야 한다.


![[ArgoCD_Github_App_Permission.png]]


# 2. Github App 설치


## 2.1 Install 버튼 클릭

생성된 Github App을 선택하면, 아래 그림과 같이 여러 설정을 추가할 수 있다. 여기서 Install App 버튼을 선택한다.


![[ArgoCD_Github_App_Install.png]]


위와 같이 해당 Github App이 설치 가능한 Account를 볼 수 있는데, 설치 대상 Organization 확인 후 Install 버튼을 누른다.


## 2.2 Repository 권한 부여

해당 App이 접근 가능한 Repository 범위를 부여한 다음 Install을 눌러 설치를 완료한다.


![[ArgoCD_Github_App_Repo_Permission.png]]



# 3. ArgoCD Github App 등록


### 3-1. Repository 탭 이동


![[ArgoCD_Repository.png]]


### 3-2. Repository 등록

CONNECT REPO 버튼을 클릭 후 Repository 정보를 등록한다.

![[ArgoCD_Repo_Github_App_Detail.png]]

1. connection method : VIA GITHUB APP
2. Type : git
3. Repository URL : k8s yaml 배포할 github의 repository 주소


그 외 Github App 등록을 위한 세부 내용 작성을 위해서는 생성한 Github App에서 여러 데이터를 참조하기 때문에 어떻게 참조할 수 있는지 하나씩 알아본다.

#### 3-2-1. Github APP ID


Github App ID는 생성한 GitHub App 수정 페이지에 접속하면, App ID가 표시되어있다. 아래예시 경우는 811637에 해당된다.

경로 : Organization > Settings > Developer Settings > OAuth Apps

![[ArgoCD_Github_App_Id.png]]


#### 3-2-2. Github App private key


3-2-1 과정을 통해 Github App 수정 페이지로 접속하여 스크롤을 내리면 Private Keys 항목이있다.

![[ArgoCD_Github_App_Private_Key.png]]

여기서 Generate a private Key를 누르면, Private Key 생성과 함께 해당 Private Key가 PEM 파일 형태로 PC에 다운로드된다.


```
-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEA1jJXluVn037G0hOJjCPRA6flUrwOYU0xr/POOWgqLIH/299E
6T3oFVvVp46dBsVle3pK1BCRjEnjt6HnaiCGuq70bBvOa5Wio/7p3osHX0e8EcBT
XixX49NbpEDBgkkxVxyWRhwiLbzVqEdWSgDqnA1hTnhjNxfmjiX4ArzSbKhcxA6g
46a4x3OJArX9YxB61dixJCoXsuHbbZEJ/JnEfbCz633X8h38aZNL8RRKxgUgtgFo
ZacZ3XBqexECRtfStpp2Onx6sDxDT1J1um7III4Nu+IM7pxyjR0cB8VXQNmuGL66
voiW34x/fGs6MRqLrqxvtb0TG87CcoMT3FLFAwIDAQABAoIBAQCrBMrWWhfJz4Ej
HiJGWBp8FsOMiUXZ/m5blAfl4fs6ShllDiDRMXJqC0bNX5qUW2spaXzxUMFFB4Hf
jk9cdtfbmfDhmFn5oCGZWuCTpOGf+4B3k918ZV9PMeQLgwB9676PVO3O0IuhhRH6
J+sHby/ipPQ6WPiudlDI0hvw454GzffuFVH8ehvSWKdPE6E+LWAurIAs/WePz2aA
7GQLNMjpJCr7yOGJVypZzg+NCw2JrZ2FMr3RbpyPDx2WDL7VEveHh3ixJJzVMyPW
0cqOdg/NCAIH6N/wpABSM9CApYXMYt1lEbA3lPgqZ3qQLYKau/aCkiUgyi4DE+1s
H4R6JhXBAoGBAPRSbHBpsu3e5QADVs1cgVmXzvklan74cUFmvV/YuVFL/MiXKglf
eSds80RMOS5jpYaQFady5dqB1gQ4Dj+ArMvtb4KMIUFZMck09lFMYTEw70xr7V7F
QsNKAyYN6RzjVSB0/W4kpUQE83JjvJEiqMiUgTRxgv9FaOwoNA7ZVFpRAoGBAOBv
THRaxwaQbrTzxbEUFCSPJBMppaeEWD7or2q8jg0wF8NKSe/3oSUFlgNr2z65sn5B
53kHcBeiEy4U2q2NPbPn8iZkiwrfc3uDHjAcme6Nu9wYAHZDZdUoXl9vOBrtWewD
tZwgN8SOdEZtY5ZlRaLl1iTu2RYmfJ0ZCZzsKcETAoGANWVqI6tGGqyTGcyhBOLJ
tj3yUws1WiiMAAInMzJXVggoZ+J5onDGNrKd+/g4qwXGIEGPKfh3eajUkDl8C67g
lPUAYOSlQ/XtZo73ok7yEuEh+26/Au5TqACd7YwuvUyFx0EqPg8uO05lskNP69xK
TQP/tOl1+ro9sxcaQYCH6fECgYEAoZZglHF7VDWPD4dnsWvEaOIKViWpGCgIJRsA
mTeyiroyka+d9kDy66XO8R2pl8q5QYAPuSrqwIk3h/kJzOShJTN9O7kuBqEFE0s+
4+LjzUaMmBVL19oEqmjLMajw2ypCkNPG4OatYD40ZzSA/Bpj/bm+6Y5yDCmflLgf
HLVIBrMCgYEAqcuvsm6lidPC0z9RDjdF1LjaspdgFWi1tujR5muVe/d7AZZ4Kesi
U9ro9y34BZ8WrRFmPMHY0I/K4wlBpfWNY4rCbzXn8v4LY9kPOZmmpEbniMvahp14
ipEv8p10ah+n25a/QFhBlPOo/zvWKm/ORCAaxf50P4h/852aDGnCK/A=
-----END RSA PRIVATE KEY-----

```


다운로드된 Private Key의 형식은 위와 같다. 위 내용이 ArgoCD에 작성해야할 내용이다.

#### 3-2-3. Github App Installation ID

Github App Installation ID는 Organization에 설치된 Github App에 부여되는 ID이다. 해당 정보는 Organization Github App 설정 화면에 접속하면 브라우저에 명시된 URL을 보고 알 수 있다. 아래의 예시는 46754780이 Installation ID이다.

경로 : Organization > Settings > Github Apps

![[ArgoCD_Github_App_Installiation_Id.png]]


