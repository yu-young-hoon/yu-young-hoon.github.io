---
layout: default
title: windows bat
parent: shell
nav_order: 206200
---

* @echo off
  ** echo 표시 끄기
* mode con cols=58 lines=32
  ** 화면 표시 모양 변경
* cls
  ** 화면 clear
* echo.
  ** 출력
* set /p menu=번호를 입력해주세요 :
  ** menu로 입력
* if "%menu%"=="1" goto _1
* goto _main
* :_main
* del
* copy nul
* echo asdf >> "filename:

### 참고링크
* windows cmd 명령어 <https://zetawiki.com/wiki/%EC%9C%88%EB%8F%84%EC%9A%B0_CMD_%EB%AA%85%EB%A0%B9%EC%96%B4_%EB%AA%A9%EB%A1%9D>
* windows bat 팁 <https://www.lesstif.com/pages/viewpage.action?pageId=17105830>
* windows bat string <https://www.dostips.com/DtTipsStringManipulation.php>
* windows bat 특수문자 <https://contain.tistory.com/entry/%EB%B0%B0%EC%B9%98%ED%8C%8C%EC%9D%BC%EB%B2%88%EC%97%AD%ED%8A%B9%EC%88%98%EB%AC%B8%EC%9E%90-%EC%B2%98%EB%A6%AC-%EB%B0%A9%EB%B2%95>
