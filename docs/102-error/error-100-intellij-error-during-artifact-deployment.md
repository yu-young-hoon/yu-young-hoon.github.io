---
layout: default
title: intellij Error during artifact deployment. See server log for details.
parent: error
nav_order: 102100
---
## 에러
intellij에서 톰캣에 빌드된 war를 제공(deploy) 하기 위한 기능을 사용중

Error during artifact deployment. See server log for details. 와 같은 에러 발생

## 해결법
stackoverflow에 답변에 나와있는 해결법을 7가지의 순서로 적어 놓았다. 간단히보면

1. 수동으로 artifact 빌드
2. artifact가 출력 예상 디렉토리에 있는지 확인
3. file -> project structure -> artifacts 로 이동
4. 문제 파일 선택
5. 출력 디렉토리가가 없다면 직접 디렉토리를 만들어 보라<br>
6. 내용이 올바른지 확인하고
7. 다시해봐라

![](/docs/attach/intellij-error-artifacts.png)
자세히 적어놓은 stackoverflow에 설명에도 나와있지만 intellij가 폴더를 자동으로 만들어 주지 않을때가 있다고 한것 처럼 나도 output의 위치를 libs 내부의 exploded폴더로 설정 해놓았는데 libs에 파일이 생성되고 있었다.

기존에 output 경로는 /Users/we/Documents/project/ad-web/build/libs/exploded/파일이름.war로 되어있었는데

변경후 /Users/we/Documents/project/ad-web/build/libs/exploded로 경로를 변경하고 폴더를 직접 생성해주자 잘 실행되었다.

## 참고링크
* https://stackoverflow.com/questions/31705700/using-intellij-to-build-war-and-deploy-to-tomcat
