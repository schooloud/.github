# SCHOOLOUD 설치 방법

본 문서는 schooloud 서비스 배포 시 설치 후 실행 방법에 대해 기술합니다.<br>
클라우드 인프라 서비스를 위한 서버3대(Backend, proxy, openstack)와 dns 연결을 위한 nhn DNS plus 서비스가 필요합니다.<br>
라이선스는 각 레포지토리를 참고해주세요!

## 목차

- <a href="profile/INSTALL_BE.md">Backend-server</a>
- <a href="profile/INSTALL_PROXY.md">Proxy-server</a>
- <a href="profile/INSTALL_OPENSTACK.md">Openstack-server</a>
- <a href="profile/INSTALL_FE.md">Frontend-server</a>

# Guideline for Conribution

**SCHOOLOUD**에 기여해주셔서 감사합니다.

아래 사항을 참고해주세요.

- [컨트리뷰션 가이드](#컨트리뷰션-가이드)
- [PR 가이드](#pr-가이드)
- [commit 가이드](#commit-가이드)
- [컨벤션 가이드](#컨벤션-가이드)

<br>

## 컨트리뷰션 가이드

### 다양한 방식으로 기여할 수 있습니다.
<br>

언제든지 편하게 issue에 의견을 올려주세요!<br> 
의견을 공유하는 것도 기여입니다.<br>
issue에서 다양한 의견을 공유하고, 추가되거나 수정되어야하는 기능을 PR로 기여하실 수도 있습니다.

<br>

## PR 가이드

- 컨트리뷰터가 아닌 경우 fork 후 PR을 요청해주세요.

1. Fork the repo to your own repo.
2. Create your branch for PR.
3. Modify the code.
4. Push your changes to your own branch.
5. Create PR.

- PR 형식은 아래와 같습니다.
- PR을 확인하면 빠른 시일 내에 리뷰와 함께 처리하도록 하겠습니다.

<예시>

---

### Description

설명

### Changes

변경사항

#### Test Checklist

테스트 항목

---
<br>

### branch 전략
기본적으로 main branch가 존재하며 PR merge를 요청하는 branch는 **develop**입니다.<br>
dev에서 분기한 branch의 이름은 **feature/이슈넘버 or xxx**, **fix/이슈넘버 or xxx** , **refactor/xxx** 로 지정해주세요.
<br>
- PR을 Merge 하기 위해선 반드시 1명 이상의 **Approve**가 필요합니다.
- PR은 **Sqush and merge** 옵션으로 merge합니다.
- main <- develop으로 Merge 시에는 **Create a merge commit** 옵션으로 Merge합니다.
- PR 제목은 아래와 같이 지어주세요. (issue가 없다면 생략해주세요)
```
  (#issue-number) 내용 요약
```
 - main <- develop PR 생성 시 develop에 merge된 pr 목록을 내용에 적어주세요.
 - main, develop branch에는 commit할 수 없습니다.
 - main은 prod에 배포하는 브랜치이기 떄문에 주의해주세요.
<br>

### 코드 리뷰 규칙

[코드 리뷰 참고 글](https://tech.kakao.com/2022/03/17/2022-newkrew-onboarding-codereview/)을 읽어주세요

- 왜 개선이 필요한지 이유를 **충분한 설명**해 주세요.
- 답을 알려주기보다는 스스로 고민하고 개선 방법을 선택할 수 있게 해주세요.
- **코드를 클린** 하게 유지하고, 일관되게 구현하도록 안내해 주세요.
- 리뷰 과정이 숙제검사가 아닌 학습과정으로 느낄 수 있게 리뷰해 주세요.
- 리뷰를 위한 리뷰를 하지 마세요. 피드백 할 게 없으면 **칭찬**해 주세요.

리뷰어의 책임이 50%라는 마음으로 리뷰를 부탁드립니다.
<br><br>

## commit 가이드

Commit 양식은 [해당 사이트](https://www.conventionalcommits.org/en/v1.0.0/#summary)를 참고해주세요.


```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

- 위의 양식을 준수하며 제목과 본문은 **한글**로 작성해주세요. <br>
- type은 **영어**로 작성해주세요.


예시 )

```
feat: 프로젝트 삭제 기능 추가

//본문은 한줄 띄워주세요
xxx 관리자의 수월한 프로젝트 관리를 위해....
```
- 커밋 로그를 보고 흐름을 이해할 수 있도록 작성 부탁드려요.
- 명확한 제목과 자세한 본문 작성을 부탁드려요.

<br><br>


## 컨벤션 가이드

[구글 코딩 컨벤션](https://github.com/google/styleguide)을 따라주세요
<br>
- JAVA: https://github.com/google/styleguide/blob/gh-pages/intellij-java-google-style.xml
- Python: https://peps.python.org/pep-0008/
- Other: ...
<br><br>

Intellij의 경우 컨벤션 auto-setting 방법이 존재하며 세팅을 해놓는 것을 추천드립니다<br>
클린 코드를 함께 고민보아요!






