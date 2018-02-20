---
layout: post
title: "언리얼 소스 빌드 및 배포하기"
description: ""
tags: [unrealengine]
comments: true
---

언리얼 소스 빌드 후 팀에서 사용하기 위해 배포하는 경우 해줘야 하는 작업


## InstalledBuild.txt
언리얼을 소스로 빌드하면
> /Engine/Build/SourceDistribution.txt

파일이 생기는데 배포 시에는 이 파일은 삭제하고
> /Engine/Build/InstalledBuild.txt

파일을 넣어줘야 에디터 실행 시 엔진을 빌드(?!)하려고 하지 않는다.

## 빌드된 엔진 레지스트리 등록

> [HKEY_CURRENT_USER\Software\Epic Games\Unreal Engine\Builds]
>
> "**{E68769AA-4436-FC9E-FE7C-43846A223E9F}**"="**C:/UE/UnrealEngine/**"

**{E68769AA-4436-FC9E-FE7C-43846A223E9F}** - 엔진 버전

**C:/UE/UnrealEngine/** - 엔진 설치된 경로

빌드 배포한 엔진을 사용하는 프로젝트의 .uproject 파일은 EngineAssociation 항목에 4.19 등의 버전 대신 uuid를 사용한다

레지스트리에서 uuid에 경로에 있는 엔진을 찾아서 빌드/실행에 사용하는 것

### .uproject
<pre>
{
	"FileVersion": 3,
	"EngineAssociation": "**{E68769AA-4436-FC9E-FE7C-43846A223E9F}**",
	"Category": "",
	"Description": "",
...
</pre>

### 배포해야하는 파일

일부 불필요한 파일이 다수 포함되어 있을 수 있지만..

딱히 문서도 없고 그걸 다 파볼 여유도 없어서 적당한 용량 선에서 합의봄

* /Engine/
  * \- /Documentaion
  * /Build
    * \- SourceDistribution.txt
    * \+ InstalledBuild.txt
    