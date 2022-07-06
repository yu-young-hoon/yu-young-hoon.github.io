---
layout: default
title: HTML/CSS form 안에 있는 button의 자동 submit 막기
parent: htmlcss
nav_order: 205101
---

```html
<form class="f_login" method="POST" action="/">
    <input id="i_id" placeholder="ID"></input>
    <input type="password" id="i_password"></input>
    <button class="b_login">로그인</button>
</form>
```
* 이런 형태의 form이 있을때 버튼을 눌르면 click 이벤트가 실행되도록 코드를 작성하게되면 javascript코드와는 상관 없이 submit이 되버리게 된다.

```js
$(".b_login").click(function () {
    if ($("#i_id").val() == "" || $("#i_id").val().length > 50) {
        alert("ID를 재입력해주십시오. ID는 50글자 제한입니다.");
        return;
    }
    $(".f_login").submit();
});
```
* 위와 같이 작성하더라도 submit이 되게 되고 클라이언트 단에서의 문법검사가 진행되지 않고 전송해버리게 된다.

```html

<form class="f_login" method="POST" action="/">
    <input id="i_id" placeholder="ID"></input>
    <input type="password" id="i_password"></input>
    <button type="button" class="b_login">로그인</button>
</form>
```
* 이런 문제를 해결하기 위해서는 button에 type="button"의 attribute를 추가해주면 된다.
