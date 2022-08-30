---
layout: default
title: Issue intellij queryDsl Q파일 인식 못하는 문제
parent: issue
nav_order: 101100
---

## Q파일 인식이 안되고 generated source root로 등록이 안되있을때 해결 방법

![](../../attach/intellij-queryDsl01.png)
* File -> Invalidate Caches/Restart 캐시 무효화하고 다시 시작

![](../../attach/intellij-queryDsl02.png)
* 생성된 Q파일 폴더 오른쪽 클릭

![](../../attach/intellij-queryDsl03.png)
* generated source root 선택

### 참고링크
* https://stackoverflow.com/questions/26952078/intellij-cannot-resolve-symbol-on-import
